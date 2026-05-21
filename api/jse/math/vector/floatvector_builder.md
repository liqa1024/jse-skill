# FloatVector.Builder

> `jse.math.vector.FloatVector.Builder`

**核心职能**：`FloatVector` 的构造期动态追加器。`extends FloatList`，用于在长度尚未确定时收集 float 数据，最后 `build()` 生成固定尺寸 `FloatVector`；`build()` 后内部数据置空，Builder 失效。Groovy 脚本可用 `b << value` / `b << vector` 追加。

```java
FloatVector build()

Builder append(float aValue)
Builder appendAll(IFloatVector aVector)
@VisibleForTesting Builder leftShift(float aValue)
@VisibleForTesting Builder leftShift(IFloatVector aVector)
```
