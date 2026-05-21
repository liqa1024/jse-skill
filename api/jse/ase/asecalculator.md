# AseCalculator

> `jse.ase.AseCalculator`

**核心职能**：`implements IPotential`。将 ASE 的 `Calculator` 对象包装为 jse 的 `IPotential`。通过 ASE atoms 的 `get_potential_energy`/`get_forces`/`get_stress` 方法计算能量/力/维里，自动检测 `implemented_properties` 判断支持项。`new AseCalculator(pyCalc)` / `new AseCalculator(pyCalc, keepLastAtoms)`。

```java
// 构造器
AseCalculator(PyObject aCalc)                      // 不保留临时 atoms
AseCalculator(PyObject aCalc, boolean aKeepLastAtoms) // keep=true 可通过 lastAtoms() 获取

// === 生命周期 ===
boolean isClosed()
void close() throws Exception                      // 尝试调用 release()/close() 关闭 ASE 计算器
@Nullable PyObject lastAtoms()                     // 上次计算创建的 atoms（需 keepLastAtoms=true）

// === IPotential 实现 ===
boolean perAtomEnergySupport()                     // 是否支持 energies（每原子能量）
boolean perAtomStressSupport()                     // 是否支持 stresses（每原子应力）
// 不支持 centroidPerAtomStressSupport（9 列应力）
// calEnergyForceVirials(...) — 完整实现：自动调用 ASE get_potential_energy/get_forces/get_stress(stresses)
double calEnergyAt(IAtomData, ISlice)               // 不支持 → UnsupportedOperationException
PyObject ase()                                      // 返回内部包装的 PyObject

// === IPotential default 方法自动继承 ===
// calEnergies/calEnergy/calForces/calStresses/calStress (便捷入口)
// calEnergyDiffMove/calEnergyDiffSwap/calEnergyDiffFlip (不支持部分原子能量)
```
