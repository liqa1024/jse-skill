# `jse.plot`

> 基于 JFreeChart 的二维折线图绘制框架——提供 matplotlib 风格的 chainable API。核心接口 `IPlotter` 支持 `plot`/`loglog`/`semilogx`/`semilogy` 四种绘图模式，每种 30 个重载覆盖 `double[]`/`IVector`/`IFunc1`/`Iterable`/`Collection` 等参数组合。线条 (`ILine`)、图例 (`ILegend`)、图形 (`IFigure`) 均支持链式属性设置。Groovy 用户通常通过 `UT.Plot` 静态门面调用。

## 架构总览 (Architecture)

```
IPlotter — 绘制器接口 (30×4 plot 重载 + 显示/保存/字体/范围/刻度/边距/轴类型)
IFigure — 图形窗口接口 (show 返回值)
ILine — 线条接口 (颜色/线型/线宽/标记形状/标记颜色/标记大小/填充/图例可见性)
ILegend — 图例接口 (显示/隐藏/位置/字体/最大尺寸/方向)
IResizable — 可调整大小接口 (getSize/setSize)
  → IResizableShape (extends Shape)
  → IResizableStroke (extends Stroke)

AbstractLine (abstract, implements ILine) — ILine 骨架，持有 IResizableStroke/IResizableShape
AbstractResizableShape (abstract, implements IResizableShape) — 可调大小 Shape 骨架
AbstractResizableStroke (abstract, implements IResizableStroke) — 可调大小 Stroke 骨架

PlotterJFree (implements IPlotter) — JFreeChart 实现，含 LineJFree/FigureJFree/LegendJFree 内部类

Plotters — 静态工厂 (get/jFree)
Anchors — AnchorType 枚举 + toAnchorType 字符串转换
Colors — 颜色常量 + COLOR(idx)/toColor 字符串转换
Shapes — MarkerType 枚举 + toShape/toMarkerType + 8 种 Marker Shape 实现
Strokes — LineType 枚举 + toStroke/toLineType + 7 种 Stroke 实现
```
