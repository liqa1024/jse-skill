# UT.Math

> `jse.code.UT.Math`

**核心职能**：`@VisibleForTesting` 静态门面——标量/向量/矩阵逐元素数学函数（sqrt/exp/log/pow/sin/cos 及反双曲函数）、归约统计、随机数生成与数学常量。底层 API 详见 `jse.math`。

```java
// === 常量 ===
static final double PI, pi = PI
static final double E, e = E
static final IComplexDouble i1, j1 = i1
static final double NaN, nan = NaN
static final double Inf, inf = Inf

// === 标量函数 — 委托 jafama FastMath ===
static double sqrt(double aValue)
static double cbrt(double aValue)
static double hypot(double aX, double aY)
static double hypot(double aX, double aY, double aZ)
static double exp(double aValue)
static double log(double aValue)
static double log10(double aValue)
static double pow(double aValue, double aPower)
static double powFast(double aValue, int aPower)
static double pow2(double aValue)
static double pow3(double aValue)
static double sin(double aValue) / cos / tan
static double asin(double aValue) / acos / atan
static double atan2(double aY, double aX)
static double sinh(double aValue) / cosh / tanh
static double asinh(double aValue) / acosh / atanh
static double floor(double aValue) / ceil
static long round(double aValue)
static double toRange(double aMin, double aMax, double aValue)
static int toRange(int aMin, int aMax, int aValue)
static long toRange(long aMin, long aMax, long aValue)
static double abs(double aValue)
static double min(double aLHS, double aRHS) / max

// 随机数
static double rand()
static double randn()
static int randi(int aBound)
static IRandom rng(long aSeed)
static IRandom rng()

// === IVector 逐元素 — 上述标量函数均有一致命名的 IVector 版本 ===
// 一元映射: sqrt/cbrt/exp/log/log10/pow2/pow3/sin/cos/tan/asin/acos/atan/
//           sinh/cosh/tanh/asinh/acosh/atanh/floor/ceil/round/abs
static IVector sqrt(IVector aVec)
// ... 以上全部模式: aVec.operation().map(Math::xxx)

// 带标量参数: pow/powFast/toRange
static IVector pow(IVector aVec, double aPower)
static IVector powFast(IVector aVec, int aPower)
static IVector toRange(double aMin, double aMax, IVector aVec)

// 二元 hypot — 3 种组合 (Vec+Scalar, Scalar+Vec, Vec+Vec)
static IVector hypot(IVector aX, double aY)
static IVector hypot(double aX, IVector aY)
static IVector hypot(IVector aX, IVector aY)

// 三元 hypot — 7 种重载 (任意参数位可为 IVector)
static IVector hypot(IVector aX, double aY, double aZ)
static IVector hypot(double aX, IVector aY, double aZ)
static IVector hypot(double aX, double aY, IVector aZ)
static IVector hypot(IVector aX, IVector aY, double aZ)
static IVector hypot(IVector aX, double aY, IVector aZ)
static IVector hypot(double aX, IVector aY, IVector aZ)
static IVector hypot(IVector aX, IVector aY, IVector aZ)

// 二元 atan2 — 3 种组合
static IVector atan2(IVector aY, double aX)
static IVector atan2(double aY, IVector aX)
static IVector atan2(IVector aY, IVector aX)

// === IVector 归约 / 累积 ===
static double sum(IVector aVec) / mean / prod / min / max
static IVector cumsum(IVector aVec) / cummean / cumprod / cummin / cummax

// === IVector 向量运算 ===
static double dot(IVector aVec)                  // 自身内积
static double dot(IVector aLHS, IVector aRHS)    // 两点积
static double norm(IVector aVec)                 // L2 范数
static double norm1(IVector aVec)                // L1 范数

// === IVector 创建 ===
static Vector zeros(int aSize) / ones / NaN
static Vector nan(int aSize)
static Vector rand(int aSize)
static Vector randn(int aSize)
static Vector randi(int aBound, int aSize)
// :note: linspace/logspace 基于累加实现，端点可能存在浮点误差
static Vector linsequence(double aStart, double aStep, int aN)
static Vector linspace(double aStart, double aEnd, int aN)
static Vector logsequence(double aStart, double aStep, int aN)
static Vector logspace(double aStart, double aEnd, int aN)

// === IMatrix 逐元素 — 与 IVector 完全一致的命名和方法模式 ===
// 一元映射: sqrt/cbrt/exp/log/log10/pow2/pow3/sin/cos/tan/asin/acos/atan/
//           sinh/cosh/tanh/asinh/acosh/atanh/floor/ceil/round/abs
static IMatrix sqrt(IMatrix aMat)
// ... 全部模式同 IVector

// 带标量参数
static IMatrix pow(IMatrix aMat, double aPower) / powFast / toRange

// 二元 hypot — 3 种组合 (Mat+Scalar, Scalar+Mat, Mat+Mat)
static IMatrix hypot(IMatrix aX, double aY)
static IMatrix hypot(double aX, IMatrix aY)
static IMatrix hypot(IMatrix aX, IMatrix aY)

// 三元 hypot — 7 种重载
static IMatrix hypot(IMatrix aX, double aY, double aZ)
// ... 其余 6 种模式同 IVector

// 二元 atan2 — 3 种组合
static IMatrix atan2(IMatrix aY, double aX) / atan2(double aY, IMatrix aX) / atan2(IMatrix aY, IMatrix aX)

// === IMatrix 归约 ===
static double sum(IMatrix aMat) / mean / min / max
static IVector sumOfCols(IMatrix aMat) / sumOfRows / meanOfCols / meanOfRows

// === IMatrix 创建 ===
static RowMatrix zeros(int aRowNum, int aColNum) / ones / NaN
static RowMatrix nan(int aRowNum, int aColNum)
static RowMatrix rand(int aRowNum, int aColNum)
static RowMatrix randn(int aRowNum, int aColNum)
static RowMatrix randi(int aBound, int aRowNum, int aColNum)
static RowMatrix diag(IVector aVec)
static IVector diag(IMatrix aMat)
static IVector diag(IMatrix aMat, int aShift)

// === 特殊函数 ===
static double legendre(int aL, int aM, double aX)
static IVector legendre(int aL, int aM, IVector aX)
static IMatrix legendre(int aL, int aM, IMatrix aX)
```
