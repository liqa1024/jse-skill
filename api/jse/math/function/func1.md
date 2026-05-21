# Func1

> `jse.math.function.Func1`

**核心职能**：创建一维函数的静态工厂。默认产出 `ConstBoundFunc1`。私有构造器，纯静态方法类。

```java
static ConstBoundFunc1 ones/zeros(double x0, double dx, int Nx)       // 全1/全0等距
static UnequalIntervalFunc1 zeros(int Nx, IVectorGetter xGetter)      // 全0非等距
static ConstBoundFunc1 from(double x0, double dx, int Nx, IFunc1Subs) // 从lambda生成等距
static ConstBoundFunc1 from(double x0, double dx, double[]/IVector/Iterable) // 从数据生成
static UnequalIntervalFunc1 from(IVector x, IFunc1Subs/IVector f)     // 从X+F生成非等距
static ZeroBoundSymmetryFunc1 deltaG(double sigma, double mu, double resolution) // 高斯 Dirac Delta
static ZeroBoundFunc1 distFrom(IHasDoubleIterator data, double start, double end, int N) // 直方图
static ZeroBoundFunc1 distFrom_G(...)                                  // 高斯展宽直方图
```
