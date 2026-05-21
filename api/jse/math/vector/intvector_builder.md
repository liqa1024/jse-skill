# IntVector.Builder

> `jse.math.vector.IntVector.Builder`

**核心职能**：`IntVector` 的构造期动态追加器。`extends IntList`，用于在长度尚未确定时收集 int 数据，最后 `build()` 生成固定尺寸 `IntVector`；`build()` 后内部数据置空，Builder 失效。Groovy 脚本可用 `b << value` / `b << vector` 追加。

```java
IntVector build()

Builder append(int aValue)
Builder appendAll(IIntVector aVector)
@VisibleForTesting Builder leftShift(int aValue)
@VisibleForTesting Builder leftShift(IIntVector aVector)
```
