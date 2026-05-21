# Func2

> `jse.math.function.Func2`

```java
static ConstBoundFunc2 zeros(double x0, double dx, int N)             // 正方形全0
static ConstBoundFunc2 zeros(double x0, double y0, double dx, double dy, int Nx, int Ny) // 矩形全0
static ZeroBoundSymmetryFunc2 deltaG(double sigma, double mu, double resolution) // 二维高斯Delta
static ZeroBoundFunc2 distFrom(IHasDoubleIterator dx, IHasDoubleIterator dy, ...)    // 二维直方图
static ZeroBoundFunc2 distFrom_G(...)                                  // 高斯展宽二维直方图
```
