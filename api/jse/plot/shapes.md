# Shapes

> `jse.plot.Shapes`

**核心职能**：定义 `MarkerType` 枚举（NULL/CIRCLE/PLUS/ASTERISK/CROSS/SQUARE/DIAMOND/TRIANGLE/ELSE），提供 `toMarkerType(String)` 字符串转换（支持 "o"/"circle"/"+"/"plus"/"*"/"asterisk"/"x"/"cross"/"s"/"square"/"d"/"diamond"/"^"/"triangle"/"none"/"null"）和 `toShape(MarkerType, double)` 工厂方法。含 8 种内部 Shape 实现类，视觉尺寸经缩放系数校正一致。

```java
// === MarkerType 枚举 ===
enum MarkerType { NULL, CIRCLE, PLUS, ASTERISK, CROSS, SQUARE, DIAMOND, TRIANGLE, ELSE }

static MarkerType toMarkerType(String aMarkerType)
static IResizableShape toShape(MarkerType aMarkerType, double aMarkerSize)

// === Shape 实现类 ===
static class NullShape extends AbstractResizableShape     // 空形状
static class Square extends Rectangle2D.Double implements IResizableShape  // 正方形
static class Circle extends Ellipse2D.Double implements IResizableShape    // 圆形 (×1.10 视觉校正)
static class Plus extends AbstractResizableShape          // 十字 (×1.40)
static class Asterisk extends AbstractResizableShape      // 星号 (×1.30)
static class Cross extends AbstractResizableShape         // 叉号 (×1.40)
static class Diamond extends AbstractResizableShape       // 菱形 (×0.90)
static class Triangle extends AbstractResizableShape      // 三角形

// === 默认值 ===
static final MarkerType DEFAULT_MARKER_TYPE = MarkerType.NULL
static final double DEFAULT_MARKER_SIZE = 12.0
```
