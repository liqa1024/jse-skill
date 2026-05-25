# jse — 势函数基础

`IPotential` 定义 jse 中势函数的统一计算协议——给定 `IAtomData`，计算能量、力、维里应力。`IPairPotential` 在此基础上限制为基于近邻列表的 pair-style 势。

> **类引用**：`IPotential`=`jse.atom.IPotential`，`IPairPotential`=`jse.atom.IPairPotential`，`APC`=`jse.atom.APC`，`IAtomData`=`jse.atom.IAtomData`，`IVector`=`jse.math.vector.IVector`，`RowMatrix`=`jse.math.matrix.RowMatrix`，`LJ`=`jse.atom.pot.LJ`

## 整体架构

```
IPotential                              ← 基础协议：能量/力/维里 + 便捷入口 + 能量差优化
  └── IPairPotential                    ← pair-style 协议：基于近邻列表，配合 APC 加速
        ├── LJ / Soft / EAM             ← jse 纯 Java 实现（详见 pot2.md）
        └── LmpPotential / AseCalculator ← 包装为 IPotential 的 LAMMPS/ASE 计算器（详见 lmp.md / ase.md）
```

`IPotential` 实现了 `AutoCloseable`，但内部资源会在 GC 时自动释放，因此 Groovy 脚本中**无需手动 close**。

与 ASE 计算器不同，`IPotential` 不持有结构状态——每次调用直接传入 `IAtomData` 即时计算。如需一次性获取多种输出，用 `calEnergyForceVirials` 一次遍历完成，避免多次重复计算。

## IPotential — 基础协议

`calEnergyForceVirials` 为底层核心——所有便捷方法内部委托至此，每个输出参数可为 `null` 跳过计算。脚本中优先使用便捷入口：

```groovy
IPotential pot = ...
IAtomData data = ...

double E = pot.calEnergy(data)                       // 总能量
IVector E_per_atom = pot.calEnergies(data)           // 每原子能量
RowMatrix forces = pot.calForces(data)               // 力矩阵 (natoms × 3)
def (sxx, syy, szz, sxy, sxz, syz) = pot.calStress(data)  // xx, yy, zz, xy, xz, yz
```

`perAtomEnergySupport()`/`perAtomStressSupport()`/`centroidPerAtomStressSupport()` 声明能力边界——并非所有后端都支持每原子输出或 9 分量 centroid stress。

## IPairPotential — pair-style 协议

jse 内置的 LJ、Soft、EAM 势均实现 `IPairPotential`。Pair-style 势基于近邻列表，提供 APC 版本的计算入口，共享已构建的 NCL 网格避免重复开销：

```groovy
IPairPotential pot = new LJ(0.5d, 3.0d, 6.0d)
def apc = APC.of(data)

double E = pot.calEnergy(apc)                        // 通过 APC 计算
RowMatrix forces = pot.calForces(apc)
```

传入 APC 时注意种类映射——`calEnergy(data)` 等自动从 `data` 检测种类数并匹配势参数，而使用 `calEnergy(apc)` 则可能需要通过 `IntUnaryOperator typeMap` 参数显式指定映射。

`rcutMax()` 声明最大截断半径，用于能量差优化的局部近邻筛选（见下节）。`NEIGHBOR_LIST_HALF` 等标志声明内核的遍历方式——引入新 pair-style 实现时需正确覆写以匹配实际近邻遍历逻辑。

### 能量差优化

`calEnergyDiffMove`/`calEnergyDiffSwap`/`calEnergyDiffFlip` 为 `IPairPotential` 专用——利用 `rcutMax` + APC 的 NCL 网格仅重算受影响的局部近邻，大幅加速 MC 模拟：

```groovy
def apc = APC.of(data)
double dE = pot.calEnergyDiffMove(apc, idx, dx, dy, dz)     // 位移试探
double dE = pot.calEnergyDiffSwap(apc, idx1, idx2)           // 交换试探
double dE = pot.calEnergyDiffFlip(apc, idx, newType)         // 变种试探
```
