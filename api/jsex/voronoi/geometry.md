# Geometry

> `jsex.voronoi.Geometry`

**核心职能**：纯静态工具类（源自 Colorado School of Mines, Dave Hale）。实现 Jonathan Shewchuk 自适应精度算法的核心谓词——先用快速方法计算，若舍入误差可能影响结果则回退到 exact 算法（使用 `DoublePair` 的高精度展开运算）。用于 Voronoi/Delaunay 构造中的方向判定与外接球测试。

```java
// === 球体与平面判定（快速 + exact 自适应回退） ===
static double leftOfPlane(double xa, double ya, double za, double xb, double yb, double zb, double xc, double yc, double zc, double xd, double yd, double zd)
static double inSphere(double xa, double ya, double za, double xb, double yb, double zb, double xc, double yc, double zc, double xd, double yd, double zd, double xe, double ye, double ze)

// === 几何计算 ===
static void centerSphere(double xa, double ya, double za, double xb, double yb, double zb, double xc, double yc, double zc, double xd, double yd, double zd, XYZ po)
```

> `leftOfPlane`: 正值=点在平面左侧 (CCW)，`inSphere`: 正值=点在球内，`centerSphere`: 将 4 点外接球心写入 `po`
