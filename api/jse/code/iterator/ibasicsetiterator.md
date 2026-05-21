# I{Type}SetIterator

> `jse.code.iterator`

**核心职能**：同时继承对应只读迭代器和只写迭代器，兼具 `next()` 读取和 `set`/`nextAndSet` 写入能力。`IComplexDoubleSetIterator` 额外 `extends ISettableComplexDouble`。

```java
// IDoubleSetIterator (extends IDoubleIterator + IDoubleSetOnlyIterator)
// 继承 next()/hasNext() + set/nextAndSet 全部方法
```

其余 5 种：`IBooleanSetIterator`, `IIntSetIterator`, `ILongSetIterator`, `IFloatSetIterator`, `IComplexDoubleSetIterator`。
