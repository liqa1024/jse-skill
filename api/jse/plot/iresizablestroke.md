# IResizableStroke

> `jse.plot.IResizableStroke`

**核心职能**：组合接口，同时继承 `IResizable` 和 `java.awt.Stroke`。用于可在运行时调整宽度的 Line 线条笔触。继承自 `IResizable` 的 `getSize`/`setSize` 方法和 `java.awt.Stroke` 的 `createStrokedShape` 方法。

```java
// 继承 IResizable:
double getSize()
void setSize(double aSize)

// 继承 java.awt.Stroke:
Shape createStrokedShape(Shape p)
```
