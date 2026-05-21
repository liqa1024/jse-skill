# VoronoiStaticExtensions

> `jsex.voronoi.VoronoiStaticExtensions`

**核心职能**：静态扩展方法，将 Voronoi 几何谓词注入 `MathEX.Graph`（`self` 参数为扩展接收者，通常为 `null`）。委托 `Geometry` 的鲁棒实现。通过 `IXYZ.x()/.y()/.z()` 桥接坐标。

```java
static double leftOfPlane(MathEX.Graph self, IXYZ aA, IXYZ aB, IXYZ aC, IXYZ aD)
static double inSphere(MathEX.Graph self, IXYZ aA, IXYZ aB, IXYZ aC, IXYZ aD, IXYZ aE)
static XYZ centerSphere(MathEX.Graph self, IXYZ aA, IXYZ aB, IXYZ aC, IXYZ aD)
```
