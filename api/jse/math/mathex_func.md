# MathEX.Func

> `jse.math.MathEX.Func`

**核心职能**：线性插值、Chebyshev 多项式、连带 Legendre 多项式、球谐函数（复/实、单/全 l）、Wigner 3-j 符号、Clebsch-Gordan 系数、阶乘。

```java
// 线性插值
static double interp1(double x1, double x2, double f1, double f2, double xq)

// Chebyshev 多项式（递推递归）
static double chebyshev(int n, double x)            // 第一类 Tn
static double chebyshev2(int n, double x)           // 第二类 Un

// 连带 Legendre 多项式（matlab 定义）
static double legendre(int l, int m, double x)

// 球谐函数 — 单个 (l,m) → ComplexDouble
static ComplexDouble sphericalHarmonics(int l, int m, double theta, double phi)
static ComplexDouble sphericalHarmonics3(int l, int m, double x, double y, double z)
// 球谐函数 — 固定 l，所有 m=-l..l → ComplexVector[2l+1]
static ComplexVector sphericalHarmonics(int l, double theta, double phi)
static ComplexVector sphericalHarmonics3(int l, double x, double y, double z)
// 球谐函数 — 所有 l=0..LMax → ComplexVector[(LMax+1)²]
static ComplexVector sphericalHarmonicsFull(int lMax, double theta, double phi)
static ComplexVector sphericalHarmonicsFull3(int lMax, double x, double y, double z)

// 实球谐函数（参考 arXiv:1410.1748 定义）
static Vector realSphericalHarmonics(int l, double theta, double phi)
static Vector realSphericalHarmonics3(int l, double x, double y, double z)
static Vector realSphericalHarmonicsFull(int lMax, double theta, double phi)
static Vector realSphericalHarmonicsFull3(int lMax, double x, double y, double z)

// Wigner 3-j 符号（整数输入）
static double wigner3j(int j1, int j2, int j3, int m1, int m2, int m3)

// Clebsch-Gordan 系数（整数输入）
static double clebschGordan(int j1, int j2, int j, int m1, int m2, int m)

// 阶乘（返回 double 避免整型溢出）
static double factorial(int n)
```
