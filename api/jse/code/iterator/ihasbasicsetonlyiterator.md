# IHas{Type}SetOnlyIterator

> `jse.code.iterator`

**核心职能**：6 种 `@FunctionalInterface`，提供 `setIterator()` 获取只写迭代器。含 `assign(Supplier)` 批量写入默认方法。`IHasComplexDoubleSetOnlyIterator` 额外提供 3 种 `assign` 重载。

```java
// IHasDoubleSetOnlyIterator
IDoubleSetOnlyIterator setIterator()
default void assign(DoubleSupplier aSup)
```

其余 5 种：`IHasBooleanSetOnlyIterator`, `IHasIntSetOnlyIterator`, `IHasLongSetOnlyIterator`, `IHasFloatSetOnlyIterator`, `IHasComplexDoubleSetOnlyIterator`。
