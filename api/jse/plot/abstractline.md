# AbstractLine

> `jse.plot.AbstractLine`

**核心职能**：持有 `IResizableStroke`（线型 Stroke）和 `IResizableShape`（标记 Shape），通过 `toStroke`/`toShape` 将 `LineType`/`MarkerType` 枚举转为 Java AWT 对象。子类需重写 `onLineTypeChange`/`onMarkerTypeChange`/`onLineWidthChange`/`onMarkerSizeChange`/`onMarkerEdgeWidthChange` 五个回调。

```java
protected abstract void onLineTypeChange(LineType aOldLineType, LineType aNewLineType)
protected abstract void onMarkerTypeChange(MarkerType aOldMarkerType, MarkerType aNewMarkerType)
protected abstract void onLineWidthChange(double aOldLineWidth, double aNewLineWidth)
protected abstract void onMarkerSizeChange(double aOldMarkerSize, double aNewMarkerSize)
protected abstract void onMarkerEdgeWidthChange(double aOldEdgeWidth, double aNewEdgeWidth)

// 内部字段
protected IResizableStroke mLineStroke
protected IResizableShape mMarkerShape
protected IResizableStroke mMarkerStroke
protected LineType mLineType
protected MarkerType mMarkerType
```
