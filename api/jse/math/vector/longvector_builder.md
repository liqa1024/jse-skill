# LongVector.Builder

> `jse.math.vector.LongVector.Builder`

**核心职能**：`LongVector` 的构造期动态追加器。`extends LongList`，用于在长度尚未确定时收集 long 数据，最后 `build()` 生成固定尺寸 `LongVector`；`build()` 后内部数据置空，Builder 失效。Groovy 脚本可用 `b << value` / `b << vector` 追加。

```java
LongVector build()

Builder append(long aValue)
Builder appendAll(ILongVector aVector)
@VisibleForTesting Builder leftShift(long aValue)
@VisibleForTesting Builder leftShift(ILongVector aVector)
```
