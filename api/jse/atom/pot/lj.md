# LJ

> `jse.atom.pot.LJ`

**核心职能**：`implements IPairPotential`。`E = 4ε[(σ/r)^12 - (σ/r)^6]`，支持单一参数或种类依赖（下三角矩阵），可启用截断处能量平移。`new LJ(eps, sigma, rCut)` / `new LJ(eps[][], sigma[][], rCut[][])`。

```java
// 构造器（单一参数）
LJ(double epsilon, double sigma, double rCut)
// 构造器（种类依赖，下三角矩阵）
LJ(double[][] epsilon, double[][] sigma, double[][] rCut, String[] symbols)
LJ(double[][] epsilon, double[][] sigma, double[][] rCut)  // 无符号

// IPairPotential 实现
int ntypes()                         // -1 单一参数, >0 种类依赖
boolean hasSymbol()                  // 仅种类依赖版 true
String symbol(int)
double rcutMax()
boolean manybody()                   // false（两体势）
boolean neighborListChecked()        // true
boolean neighborListHalf()           // true
boolean shift()                      // 当前是否能量平移
LJ setShift(boolean) / setShift()    // 设置能量平移（截断处平滑归零）
int nthreads()
LJ setNthreads(int)
void calEnergy(int, INeighborListGetter, IEnergyAccumulator)
void calEnergyForceVirial(int, INeighborListGetter, IEnergyAccumulator?, IForceAccumulator?, IVirialAccumulator?)
```
