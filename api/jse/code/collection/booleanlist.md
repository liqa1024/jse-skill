# BooleanList

> `jse.code.collection.BooleanList`

**核心职能**：以 `boolean[]` 为后端的动态数组，实现 `IDataShell`。`new BooleanList()` 或 `new BooleanList(int initSize)`。

```java
BooleanList() / BooleanList(int initSize)
boolean get(int) / void set(int, boolean)
void add(boolean) / void addZeros(int)
void ensureCapacity(int) / void trimToSize() / void clear()
void forEach(BooleanConsumer)
List<Boolean> asList()
LogicalVector asVec()
LogicalVector copy2vec()
BooleanList copy()
NDArray<boolean[]> numpy()
BooleanList append(boolean) / appendAll(ILogicalVector)
```
