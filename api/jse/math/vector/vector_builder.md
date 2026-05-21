# Vector.Builder

> `jse.math.vector.Vector.Builder`

**核心职能**：`Vector` 的构造期动态追加器。`extends DoubleList`，用于在长度尚未确定时收集 double 数据，最后 `build()` 生成固定尺寸 `Vector`；`build()` 后内部数据置空，Builder 失效。Groovy 脚本可用 `b << value` / `b << vector` 追加。

```java
// === 实例方法 ===
Vector build()

@VisibleForTesting Builder leftShift(double aValue)
@VisibleForTesting Builder leftShift(IVector aVector)
```

同一模式也存在于其他具体向量实现：

| 类 | Builder 继承 | 追加值 |
|---|---|---|
| `IntVector.Builder` | `IntList` | `int` / `IIntVector` |
| `LogicalVector.Builder` | `BooleanList` | `boolean` / `ILogicalVector` |
| `LongVector.Builder` | `LongList` | `long` / `ILongVector` |
| `FloatVector.Builder` | `FloatList` | `float` / `IFloatVector` |
| `ComplexVector.Builder` | `ComplexDoubleList` | `IComplexDouble` / `IComplexVector` |
