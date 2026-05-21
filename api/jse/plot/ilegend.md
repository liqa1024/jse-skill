# ILegend

> `jse.plot.ILegend`

**核心职能**：`IPlotter.legend()` 返回的图例对象。支持显示/隐藏、位置（AnchorType 枚举 / 归一化坐标 + 锚点）、字体、最大宽高、横/纵向排列。

```java
IPlotter plotter()

boolean isShowing()
ILegend hide()
ILegend show()
ILegend font(Font aFont)
ILegend maxWidth(double aMax)
ILegend maxHeight(double aMax)
ILegend vertical()
ILegend horizontal()

ILegend location(String aLocation)
ILegend location(double aX, double aY)
ILegend location(double aX, double aY, String aAnchor)
ILegend location(AnchorType aLocation)
ILegend location(double aX, double aY, AnchorType aAnchor)
```
