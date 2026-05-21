# Anchors

> `jse.plot.Anchors`

**核心职能**：定义 `AnchorType` 枚举（NULL/CENTER/TOP/TOP_LEFT/TOP_RIGHT/BOTTOM/BOTTOM_LEFT/BOTTOM_RIGHT/LEFT/RIGHT），提供 `toAnchorType(String)` 字符串转换（支持 "center"/"c"/"top"/"t"/"north"/"n"/"topleft"/"tl"/"nw" 等）。

```java
enum AnchorType { NULL, CENTER, TOP, TOP_LEFT, TOP_RIGHT, BOTTOM, BOTTOM_LEFT, BOTTOM_RIGHT, LEFT, RIGHT }

static AnchorType toAnchorType(String aAnchorType)
static final AnchorType DEFAULT_ANCHOR_TYPE = AnchorType.NULL
```
