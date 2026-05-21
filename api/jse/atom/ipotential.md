# IPotential

> `jse.atom.IPotential`

**核心职能**：`extends AutoCloseable`。定义势函数的完整计算协议——能量/力/维里计算、每原子能量/应力、能量差优化（move/swap/flip），以及 ASE 计算器转换。

```java
// === 抽象方法（核心计算入口） ===
void calEnergyForceVirials(
    IAtomData aData,
    @Nullable IVector rEnergies,       // 每原子能量输出（null=不需要）
    @Nullable IVector rForcesX,        // 力 x 分量
    @Nullable IVector rForcesY,
    @Nullable IVector rForcesZ,
    @Nullable IVector rVirialsXX,      // 维里张量各分量
    @Nullable IVector rVirialsYY, @Nullable IVector rVirialsZZ,
    @Nullable IVector rVirialsXY, @Nullable IVector rVirialsXZ, @Nullable IVector rVirialsYZ,
    @Nullable IVector rVirialsYX, @Nullable IVector rVirialsZX, @Nullable IVector rVirialsZY
) throws Exception
// 任意输出参数为 null 表示不需要计算该项

double calEnergyAt(IAtomData, ISlice aIndices) throws Exception // 计算指定原子的总能量

// === 属性/配置（default） ===
boolean isClosed()                        // 是否已关闭，默认 false
void close() throws Exception             // 关闭释放资源，默认空
boolean perAtomEnergySupport()            // 是否支持每原子能量，默认 true
boolean perAtomStressSupport()            // 是否支持每原子压力，默认 true
boolean centroidPerAtomStressSupport()    // 是否支持 9 列每原子应力，默认 false

// === 便捷计算入口（default，内部 call calEnergyForceVirials） ===
Vector calEnergies(IAtomData)                           // 每原子能量向量
double calEnergy(IAtomData)                             // 总能量
RowMatrix calForces(IAtomData)                          // 每原子力矩阵 (natoms × 3)
List<Vector> calStresses(IAtomData, boolean)             // 每原子应力（可含理想气体项）
List<Vector> calStresses(IAtomData)                      // 不含理想气体项
List<Double> calStress(IAtomData, boolean)               // 总应力
List<Double> calStress(IAtomData)

// === 能量差优化（default，利用截断半径加速 MC 模拟） ===
double calEnergyDiffMove(ISettableAtomData/IAtomData, int idx, double dx,dy,dz, ...)
double calEnergyDiffMove(ISettableAtomData/IAtomData, int idx, IXYZ, ...)
double calEnergyDiffSwap(ISettableAtomData/IAtomData, int idx1, int idx2, ...)
double calEnergyDiffFlip(ISettableAtomData/IAtomData, int idx, int type, ...)

// === ASE 集成 ===
PyObject ase()                          // 转换为 ASE Calculator 对象
@Deprecated PyObject asAseCalculator()   // → ase()
@ApiStatus.Internal Map<String,Object> calculate_(...)  // ASE 回调（内部使用）
```
