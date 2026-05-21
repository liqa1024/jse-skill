# ShortList

> `jse.code.collection.ShortList`

**核心职能**：以 `short[]` 为后端的动态数组，实现 `IDataShell`。`new ShortList()` 或 `new ShortList(int initSize)`。

```java
ShortList() / ShortList(int initSize)
short get(int) / void set(int, short)
void add(short) / void addZeros(int)
void ensureCapacity(int) / void trimToSize() / void clear()
void forEach(ShortConsumer)
List<Short> asList()
ShortList copy()
NDArray<short[]> numpy()
ShortList append(short)
```
