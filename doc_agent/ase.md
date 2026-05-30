# jse — JSE 与 ASE 相互转换

`AseAtoms` 将 Python ASE `Atoms` 包装为 jse `IAtomData`，`AseCalculator` 将 ASE `Calculator` 包装为 jse `IPotential`；`IAtomData.ase()` / `IPotential.ase()` 提供反向导出。

> **类引用**：`AseAtoms`=`jse.ase.AseAtoms`，`AseCalculator`=`jse.ase.AseCalculator`

## 前置条件

ASE 互操作依赖 JEP（Java Embedded Python），需先执行 `jse --jnibuild` 编译 JNI native 库。**TODO(jse)**：目前无 API 可在不触发初始化的前提下检测 JNI 是否已构建，编写涉及 ASE 的脚本时注释标注 `Requires: jse --jnibuild`。Python/Groovy 混用模式参考 `python.md`。

## ASE → jse

`AseAtoms` 与 `AseCalculator` 的实现方式不同，源于两类 Python 对象的本质差异：

- **AseAtoms** — `of(pyAtoms)` 时对 Python 数据做**值拷贝**到 Java 矩阵，之后不持有原始 Python 对象引用。修改只影响 jse 侧副本，不会回写到 ASE 端。原子数据天然是"快照"语义，值拷贝避免了高频访问时的 JNI 开销。
- **AseCalculator** — 直接**持有 Python `Calculator` 引用**，每次调用都在内部创建临时 ASE Atoms 并委托给 Python 端的 `get_potential_energy`/`get_forces`/`get_stress`。计算器本身无状态，拷贝不现实，包装委托是唯一可行方式。

### AseAtoms — ASE Atoms 转为 IAtomData

`AseAtoms.of(pyAtoms)` 将 Python ASE `Atoms` 值拷贝为 `ISettableAtomData`：

```groovy
def pyAtoms = ...                                    // Python ASE Atoms 对象
AseAtoms atoms = AseAtoms.of(pyAtoms)
double E = pot.calEnergy(atoms)                      // 直接作为 jse IAtomData 使用
```

`AseAtoms.read(file)` 通过 `ase.io.read` 读取文件——但普通 extxyz/LAMMPS/VASP 格式优先使用 `atom2.md` 中的专用类，仅在 ASE 特有格式或需要 ASE 解析能力时走此路径。

ASE Atoms 的 `info`、`arrays`、`calc.results` 通过对应的三级键值系统访问。jse 采用了更一致的命名和使用方式，未照搬 ASE 接口：

```groovy
// info — 全局键值对（对应 ASE Atoms.info）
atoms.setInfo("config_type", "bulk")
def ct = atoms.info("config_type")

// array — 每原子键值对（对应 ASE Atoms.arrays）
atoms.setArray("forces", forcesMatrix)

// calcResult — 计算结果（对应 ASE Atoms.calc.results，有严格类型校验）
if (atoms.hasCalcResult("energy")) {
    double e = atoms.calcResult("energy")
}
```

### AseCalculator — ASE Calculator 包装

`new AseCalculator(pyCalc)` 将 Python ASE `Calculator` 包装为 `IPotential`，自动检测 `implemented_properties` 判断支持项：

```groovy
def pyCalc = ...                                    // Python ASE Calculator
IPotential asePot = new AseCalculator(pyCalc)

double E = asePot.calEnergy(data)
RowMatrix forces = asePot.calForces(data)
```

EAM/LJ/Soft 等内置势函数在 jse 中有纯 Java 实现（见 `pot2.md`），效率远高于 ASE 的 Python 实现且功能更全，仅当 ASE 提供了 jse 不支持的势函数时才使用 `AseCalculator` 包装。

如果需要在计算后保留临时 ASE Atoms 对象以供调试，使用 `new AseCalculator(pyCalc, true)`，然后通过 `lastAtoms()` 获取。注意 `AseCalculator` 不支持 `calEnergyAt`（部分原子能量）和 `centroidPerAtomStressSupport`（9 分量应力）。

## jse → ASE

`IAtomData.ase()` 将任意 jse 原子数据转为 Python ASE `Atoms`：

```groovy
def pyAtoms = data.ase()                             // IAtomData → ASE Atoms
```

`IPotential.ase()` 将 jse 势函数转为 ASE `Calculator`：

```groovy
def pyCalc = pot.ase()                               // IPotential → ASE Calculator
// 然后可以在 ASE 中直接使用
```

通过 `.ase()` 导出的对象为 `PyObject`，在 Groovy 中可直接传入 Python 调用链。
