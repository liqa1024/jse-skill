# MathEX.Fast

> `jse.math.MathEX.Fast`

**核心职能**：委托 jafama `FastMath` 的快速（非严格 IEEE 754）数学函数。精度略低于 `Math`，但速度更快。

```java
static double sqrt(double) / cbrt(double)
static double hypot(double x, double y) / hypot(double x, double y, double z)
static double exp(double) / log(double) / log10(double)
static double pow(double, double) / powFast(double, int) / pow2(double) / pow3(double)
static double sin/cos/tan/asin/acos/atan(double) / atan2(double y, double x)
static double sinh/cosh/tanh/asinh/acosh/atanh(double)
static double powQuick(double, double)                    // 更快但精度更低
static double sqrtQuick(double) / sinQuick(double) / cosQuick(double)
```
