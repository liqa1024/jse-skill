# I{Type}SetOnlyIterator

> `jse.code.iterator`

**核心职能**：6 种基本类型的只写迭代器。以 `IDoubleSetOnlyIterator` 为例，其余类型将 `double`/`Double` 互换。

```java
// IDoubleSetOnlyIterator
boolean hasNext()
void nextOnly()
void set(double aValue)
default void nextAndSet(double aValue)
```

其余 5 种：`IBooleanSetOnlyIterator`, `IIntSetOnlyIterator`, `ILongSetOnlyIterator`, `IFloatSetOnlyIterator`, `IComplexDoubleSetOnlyIterator`。
