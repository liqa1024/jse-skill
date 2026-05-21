# Colors

> `jse.plot.Colors`

**核心职能**：定义 10 色调色板 `COLORS[]`，提供 `COLOR(int aIdx)` 循环取色、`COLOR()` 自动递增取色、`toColor(String)` 字符串转 Color（支持 "red"/"r"/"RED"/"black"/"k"/"blue"/"b"/"green"/"g"/"none"/"null" 等）。

```java
static final Color COLOR_NULL          // (255,255,255,0) 透明
static Color COLOR(int aIdx)           // 循环取调色板色
static Color COLOR()                   // 自动递增取色
static Color toColor(String aColor)
static final Color DEFAULT_COLOR = COLOR(0)
```
