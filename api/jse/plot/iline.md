# ILine

> `jse.plot.ILine`

**核心职能**：`IPlotter.plot()` 返回的线条对象。支持链式设置线条颜色/线型/线宽、标记形状/颜色/大小/边缘宽度、图例可见性。颜色支持 `int`（索引取 Colors 调色板）、`double r,g,b`（0-1 归一化）、`String`（颜色名）、`Paint` 四种重载。`@VisibleForTesting` 别名提供简写形式（`width`/`type`/`marker`/`size`/`edgeSize` 等）。

```java
IPlotter plotter()

// === 线条颜色 ===
ILine color(int aIdx)
ILine color(double aR, double aG, double aB)
ILine color(String aColor)
ILine color(Paint aPaint)

// lineColor 仅设置线条颜色（不覆盖 markerColor）
ILine lineColor(int aIdx)
ILine lineColor(double aR, double aG, double aB)
ILine lineColor(String aColor)
ILine lineColor(Paint aPaint)

// === 线宽 ===
ILine lineWidth(double aLineWidth)
ILine width(double aLineWidth)            // @VisibleForTesting
ILine lineSize(double aLineWidth)         // @VisibleForTesting

// === 线型 ===
ILine lineType(LineType aLineType)
ILine lineType(String aLineType)
ILine type(LineType aLineType)            // @VisibleForTesting
ILine type(String aLineType)              // @VisibleForTesting
ILine lineStroke(Stroke aLineStroke)

// === 填充 ===
ILine fill()
ILine fill(boolean aFill)

// === 标记边缘颜色 ===
ILine markerColor(int aIdx)
ILine markerColor(double aR, double aG, double aB)
ILine markerColor(String aColor)
ILine markerColor(Paint aPaint)

// markerFaceColor 仅填充色（自动 fill）
ILine markerFaceColor(int aIdx)
ILine markerFaceColor(double aR, double aG, double aB)
ILine markerFaceColor(String aColor)
ILine markerFaceColor(Paint aPaint)

// markerEdgeColor 仅边缘色
ILine markerEdgeColor(int aIdx)
ILine markerEdgeColor(double aR, double aG, double aB)
ILine markerEdgeColor(String aColor)
ILine markerEdgeColor(Paint aPaint)

// === 标记边缘宽度 ===
ILine markerEdgeWidth(double aEdgeWidth)
ILine edgeSize(double aEdgeWidth)         // @VisibleForTesting
ILine markerEdgeSize(double aEdgeWidth)   // @VisibleForTesting
ILine edgeWidth(double aEdgeWidth)        // @VisibleForTesting

// === 标记大小 ===
ILine markerSize(double aSize)
ILine size(double aSize)                  // @VisibleForTesting

// === 标记形状 ===
ILine markerType(MarkerType aMarkerType)
ILine markerType(String aMarkerType)
ILine marker(MarkerType aMarkerType)      // @VisibleForTesting
ILine marker(String aMarkerType)          // @VisibleForTesting
ILine markerShape(Shape aMarkerShape)

// === 图例 ===
boolean isShowingLegend()
ILine hideLegend()
ILine showLegend()
```
