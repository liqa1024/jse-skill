# Soft

> `jse.atom.pot.Soft`

**核心职能**：`implements IPairPotential`。`E = A[1 + cos(πr/rc)]`（r<rc），用于推开过近原子。两体势。`new Soft(prefactor, rCut)` / `new Soft(prefactor[][], rCut[][])`。

```java
// 构造器
Soft(double prefactor, double rCut)
Soft(double[][] prefactor, double[][] rCut, String[] symbols)
Soft(double[][] prefactor, double[][] rCut)

// IPairPotential 实现
int ntypes()                         // -1 单一, >0 种类依赖
boolean hasSymbol() / String symbol(int)
double rcutMax()
boolean manybody()                   // false
boolean neighborListChecked()        // true
boolean neighborListHalf()           // true
int nthreads()
Soft setNthreads(int)
void calEnergy(...)
void calEnergyForceVirial(...)
```
