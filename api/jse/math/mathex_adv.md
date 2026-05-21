# MathEX.Adv

> `jse.math.MathEX.Adv`

**核心职能**：梯形数值积分、线性拟合（含误差估计）、BFS/DFS 团簇分析。

```java
// 梯形法数值积分
static double integral(double start, double end, int n, IFunc1Subs func)

// 线性拟合
static DoublePair lineFit(IVector x, IVector y)            // y=a+bx → {a,b}
static double lineFit0(IVector x, IVector y)               // y=bx → b
static DoubleTriplet lineFitSigma(IVector x, IVector y)    // y=a+bx+σ → {a,b,σ}

// 团簇分析
static List<IntVector> getClustersBFS(int size, IHasIntIterator points,
    IListGetter<? extends IHasIntIterator> neighborGetter)        // 广度优先
static List<IntVector> getClustersDFS(int size, IHasIntIterator points,
    IListGetter<? extends IHasIntIterator> neighborGetter)        // 深度优先
```
