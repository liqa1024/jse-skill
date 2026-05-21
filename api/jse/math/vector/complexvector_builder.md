# ComplexVector.Builder

> `jse.math.vector.ComplexVector.Builder`

**核心职能**：`ComplexVector` 的构造期动态追加器。`extends ComplexDoubleList`，用于在长度尚未确定时收集复数数据，最后 `build()` 生成固定尺寸 `ComplexVector`；`build()` 后内部数据置空，Builder 失效。Groovy 脚本可用 `b << value` / `b << vector` 追加。

```java
ComplexVector build()

Builder append(IComplexDouble aValue)
Builder appendAll(IComplexVector aVector)
@VisibleForTesting Builder leftShift(IComplexDouble aValue)
@VisibleForTesting Builder leftShift(IComplexVector aVector)
```
