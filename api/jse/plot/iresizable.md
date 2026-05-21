# IResizable

> `jse.plot.IResizable`

**核心职能**：可调整大小的图形元素基础接口。提供 `getSize`/`setSize` 用于在运行时改变图形元素（Marker 形状尺寸、Line 线条宽度）的尺寸。`IResizableShape` 和 `IResizableStroke` 继承自本接口。

```java
double getSize()
void setSize(double aSize)
```
