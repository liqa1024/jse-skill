# AbstractXYZ

> `jse.atom.AbstractXYZ`

**核心职能**：`abstract class implements IXYZ`。统一 `toString()` 格式（保留 4 位有效数字）并提供 `copy()` 默认实现。

```java
String toString()              // "(%.4g, %.4g, %.4g)"
XYZ copy()                     // new XYZ(this)
```
