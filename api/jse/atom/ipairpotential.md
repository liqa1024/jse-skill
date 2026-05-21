# IPairPotential

> `jse.atom.IPairPotential`

**核心职能**：`extends IPotential, IHasSymbol`。定义基于近邻列表的 pair-style 势函数协议。增加 APC 适配、近邻列表遍历、配置属性（线程数/截断/多体/半列表）。

```java
// === 抽象方法（近邻列表驱动） ===
void calEnergy(int nthreads, INeighborListGetter nlg, IEnergyAccumulator) throws Exception
void calEnergyForceVirial(int nthreads, INeighborListGetter nlg,
    @Nullable IEnergyAccumulator, @Nullable IForceAccumulator, @Nullable IVirialAccumulator
) throws Exception

// === 配置属性（default，实现类应覆写） ===
int nthreads()                  // 期望线程数，默认 1
double rcutMax()                // 最大截断半径，默认 -1（无优化）
boolean manybody()              // 是否多体势，默认 true
boolean neighborListChecked()   // 内核是否已检查截断，默认 false
boolean neighborListHalf()      // 内核是否使用半近邻列表（Newton's 3rd），默认 false

// === IHasSymbol 覆写 ===
int ntypes()                    // 默认 -1（无种类限制）
boolean hasSymbol()             // 默认 false
@Nullable String symbol(int)    // 默认 null

// === APC 版计算入口（default，自动管理 NeighborListGetter 生命周期） ===
void calEnergyForceVirials(APC, IVector energies, IVector fX,fY,fZ,
    IVector vXX,vYY,vZZ, vXY,vXZ,vYZ, vYX,vZX,vZY, IntUnaryOperator typeMap)
// ... 多种参数重载（12 参/15 参/18 参/无 typeMap...）
Vector calEnergies(APC, IntUnaryOperator/APC)     // 通过 APC 计算每原子能量
double calEnergy(APC, IntUnaryOperator/APC)       // 通过 APC 计算总能量
RowMatrix calForces(APC, IntUnaryOperator/APC)    // 通过 APC 计算力
List<Vector> calStresses(APC, IntUnaryOperator/APC)// 通过 APC 计算应力
List<Double> calStress(APC, IntUnaryOperator/APC)  // 通过 APC 计算总应力

// === 能量差优化（APC 版，利用截断半径加速） ===
double calEnergyDiffMove(APC, int idx, double dx,dy,dz, boolean, IntUnaryOperator) ...
double calEnergyDiffSwap(APC, int idx1, int idx2, boolean, IntUnaryOperator) ...
double calEnergyDiffFlip(APC, int idx, int type, boolean, IntUnaryOperator) ...

// === 部分能量计算 ===
@ApiStatus.Experimental void calEnergyPart(int, INeighborListGetter, IEnergyPartAccumulator)
double calEnergyAt(APC, ISlice) / calEnergyAt(IAtomData, ISlice)

// === 内部函数式接口（遍历/累加回调） ===
@FunctionalInterface interface INeighborListGetter { void forEach(int, INeighborListDo); }
@FunctionalInterface interface IEnergyAccumulator { void accept(int type, double dx,dy,dz, double r2, int j); }
@FunctionalInterface interface IForceAccumulator { void accept(int type, double dx,dy,dz, double r2, double r, int j); }
@FunctionalInterface interface IVirialAccumulator { void accept(int type, double dx,dy,dz, double r2, double r, int j); }
```
