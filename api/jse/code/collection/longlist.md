# LongList

> `jse.code.collection.LongList`

**核心职能**：以 `long[]` 为后端的动态数组，实现 `IDataShell`。`new LongList()` 或 `new LongList(int initSize)`。

```java
LongList() / LongList(int initSize)
long get(int) / void set(int, long)
void add(long) / void addZeros(int)
void ensureCapacity(int) / void trimToSize() / void clear()
void forEach(LongConsumer)
List<Long> asList()
LongVector asVec()
LongVector copy2vec()
LongList copy()
NDArray<long[]> numpy()
LongList append(long) / appendAll(ILongVector)
```
