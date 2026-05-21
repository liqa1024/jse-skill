# AbstractResizableShape

> `jse.plot.AbstractResizableShape`

**核心职能**：`IResizableShape` 的抽象骨架实现。委托 `mShape` 内部 `Shape` 对象，代理 `Shape` 全部几何查询方法。子类仅需重写 `getShape(aSize)` 工厂方法。

```java
// === 字段 ===
protected @NotNull Shape mShape
protected double mSize

// === 构造 ===
protected AbstractResizableShape(double aSize)

// === 尺寸 ===
double getSize()
void setSize(double aSize)

// === Shape 委托 ===
Rectangle getBounds()
Rectangle2D getBounds2D()
boolean contains(double x, double y)
boolean contains(Point2D p)
boolean intersects(double x, double y, double w, double h)
boolean intersects(Rectangle2D r)
boolean contains(double x, double y, double w, double h)
boolean contains(Rectangle2D r)
PathIterator getPathIterator(AffineTransform at)
PathIterator getPathIterator(AffineTransform at, double flatness)

// === 子类重写 ===
protected abstract @NotNull Shape getShape(double aSize)
```
