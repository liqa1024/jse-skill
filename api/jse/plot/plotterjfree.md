# PlotterJFree

> `jse.plot.PlotterJFree`

**核心职能**：`implements IPlotter`，基于 JFreeChart 的 `XYPlot` + `XYLineAndShapeRenderer` 实现。含三个 `protected` 内部类：`LineJFree` (extends AbstractLine)、`FigureJFree` (implements IFigure, 基于 JFrame)、`LegendJFree` (implements ILegend)。自定 `LargerTickUnitNumberAxis` 优化默认 Tick 间距。

> `LineJFree`/`FigureJFree`/`LegendJFree` 为 `protected` 内部类，通过父接口使用。

```java
// === 全局常量 ===
static final String TITLE = null
static final String X_LABEL = null
static final String Y_LABEL = null
static final Font TITLE_FONT
static final Font LABEL_FONT
static final Font LEGEND_FONT
static final Font TICK_FONT
static final double LEGEND_SIZE = 16.0
static final int WIDTH = 800
static final int HEIGHT = 600

// === 构造 ===
PlotterJFree()

// === IPlotter 全部方法实现（含 LineJFree/FigureJFree/LegendJFree） ===
// 参见 IPlotter 接口签名

// === FigureJFree (protected) — 实现 IFigure ===
// 基于 JFrame + ChartPanel，含 mInset 独立边距
// 重写 paintComponent 加锁防止并行修改错误

// === LegendJFree (protected) — 实现 ILegend ===
// 位置使用 AnchorType→RectangleAnchor 映射 + XYTitleAnnotation
// 默认 RIGHT 位置，支持任意 (x,y,anchor) 坐标 + maxWidth/maxHeight 约束

// === syncRun / syncSup / syncRunEx / syncSupEx (包可见) ===
// 窗口显示时的同步包装器，通过 JFrame.getTreeLock() 加锁
```
