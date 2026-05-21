# IResizableShape

> `jse.plot.IResizableShape`

**核心职能**：组合接口，同时继承 `IResizable` 和 `java.awt.Shape`。用于可在运行时调整大小的 Marker 形状。继承自 `IResizable` 的 `getSize`/`setSize` 方法和 `java.awt.Shape` 的全部几何查询方法（`getBounds`/`contains`/`intersects`/`getPathIterator`）。

```java
// 继承 IResizable:
double getSize()
void setSize(double aSize)

// 继承 java.awt.Shape 全部方法:
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
```
