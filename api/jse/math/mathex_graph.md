# MathEX.Graph

> `jse.math.MathEX.Graph`

**核心职能**：`@ApiStatus.Internal` — 偏向内部使用。三角形面积、射线与 2D 盒交点计算、点位置判断。

```java
// 三点组成的三角形面积（恒正）
static double area(IXYZ aA, IXYZ aB, IXYZ aC)

// 射线与 2D 矩形盒的交点
// 返回 double[n][2]：0 个交点=空数组，1 个=n×2，2 个=2×2
static double[][] interRayBox2D(
    double boxXMin, double boxYMin, double boxXMax, double boxYMax,
    double rayXFrom, double rayYFrom, double rayXTo, double rayYTo)

// 判断点在 2D 盒中的位置（返回 PosBox2D 常量）
static byte posBox2D(double x, double y, double xMin, double yMin, double xMax, double yMax)
```
