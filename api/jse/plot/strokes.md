# Strokes

> `jse.plot.Strokes`

**核心职能**：定义 `LineType` 枚举（NULL/SOLID/DASHED/DOTTED/DASH_DOTTED/DASH_DOT_DOTTED/DASH_DASH_DOTTED/ELSE），提供 `toLineType(String)` 字符串转换（支持 "-"/"solid"/"--"/"dashed"/":"/".."/"dotted"/"-."/"dash-dotted"/"-.."/"dash-dot-dotted"/"--."/"dash-dash-dotted"/"none"/"null"）和 `toStroke(LineType, double)` 工厂方法。全部使用圆角端点 + 圆角连接的 `BasicStroke`。

```java
// === LineType 枚举 ===
enum LineType { NULL, SOLID, DASHED, DOTTED, DASH_DOTTED, DASH_DOT_DOTTED, DASH_DASH_DOTTED, ELSE }

static LineType toLineType(String aLineType)
static IResizableStroke toStroke(LineType aLineType, double aLineWidth)

// === Stroke 实现类 ===
static class NullStroke extends AbstractResizableStroke       // 空笔触
static class Solid extends AbstractResizableStroke            // 实线
static class Dashed extends AbstractResizableStroke           // 虚线 (5×/3× 间距)
static class Dotted extends AbstractResizableStroke           // 点线 (1×/3× 间距)
static class DashDotted extends AbstractResizableStroke       // 点划线
static class DashDotDotted extends AbstractResizableStroke    // 点点划线
static class DashDashDotted extends AbstractResizableStroke   // 双划点线

// === 默认值 ===
static final LineType DEFAULT_LINE_TYPE = LineType.SOLID
static final double DEFAULT_LINE_WIDTH = 2.0
```
