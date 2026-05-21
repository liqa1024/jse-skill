# XYZ

> `jse.atom.XYZ`

**核心职能**：`extends AbstractSettableXYZ`。`IXYZ`/`ISettableXYZ` 的完整实现，支持 40+ 向量运算（含 2this 就地版本）。`new XYZ(x,y,z)` / `new XYZ()` / `new XYZ(IXYZ)` / `new XYZ(XYZ)`(直接访问字段) / `new XYZ(IVector)` / `static XYZ toXYZ(IXYZ)`。

```java
// 字段
double mX, mY, mZ       // 三维坐标（可直接读写）

// getter/setter（覆写 IXYZ/ISettableXYZ，返回 XYZ 以链式）
double x(), y(), z()
XYZ setX/setY/setZ(double)
XYZ setXYZ(double,double,double) / setXYZ(IXYZ)
XYZ copy()

// 向量运算（全部覆写 IXYZ default，提供高效直接实现）
// 统计: sum/mean/prod/min/max
// 内积: dot() / dot(double,double,double)
// 叉积: cross(double,double,double) / cross2this(IXYZ/XYZ/double×3)
// 混合积: mixed(double×9)
// 取反/绝对值: negative/abs + 2this 版本
// 范数: norm()/norm1()
// 加减: plus(IXYZ/XYZ/double×3) + plus2this + mplus2this(this+=rhs*mul)
// 减法: minus/lminus + 2this 版本
// 乘除: multiply/div/ldiv + 2this 版本 + 标量重载
// 距离: distance2/distance/distanceQuick/distanceMHT(IXYZ/XYZ/double×3)
// 比较: numericEqual(IXYZ/XYZ/double×3)
```
