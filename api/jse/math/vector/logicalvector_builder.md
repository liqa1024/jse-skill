# LogicalVector.Builder

> `jse.math.vector.LogicalVector.Builder`

**核心职能**：`LogicalVector` 的构造期动态追加器。`extends BooleanList`，用于在长度尚未确定时收集 boolean 数据，最后 `build()` 生成固定尺寸 `LogicalVector`；`build()` 后内部数据置空，Builder 失效。Groovy 脚本可用 `b << value` / `b << vector` 追加。

```java
LogicalVector build()

Builder append(boolean aValue)
Builder appendAll(ILogicalVector aVector)
@VisibleForTesting Builder leftShift(boolean aValue)
@VisibleForTesting Builder leftShift(ILogicalVector aVector)
```
