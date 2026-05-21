# IHas{Type}Iterator

> `jse.code.iterator`

**核心职能**：6 种 `@FunctionalInterface`，提供 `iterator()` 方法获取免装箱迭代器。含 `iterable()`→JDK Iterable、`forEach(Consumer)` 默认方法。`IHasComplexDoubleIterator` 额外提供 Groovy Closure 版 `forEach`。

```java
// IHasDoubleIterator
IDoubleIterator iterator()
default Iterable<Double> iterable()
default void forEach(DoubleConsumer aCon)
```

其余 5 种：`IHasBooleanIterator`, `IHasIntIterator`, `IHasLongIterator`, `IHasFloatIterator`, `IHasComplexDoubleIterator`。
