# IntList

> `jse.code.collection.IntList`

**核心职能**：以 `int[]` 为后端的动态数组，实现 `IDataShell` 和 `ISlice`。`new IntList()` 或 `new IntList(int initSize)`。

```java
IntList() / IntList(int initSize)
int get(int) / void set(int, int)
void add(int) / void addZeros(int)
void ensureCapacity(int) / void trimToSize() / void clear()
void forEach(IntConsumer)
List<Integer> asList()
IntVector asVec()
IntVector copy2vec()
IntList copy()
NDArray<int[]> numpy()
IntList append(int) / appendAll(IIntVector)
int removeLast()
boolean contains(int)
```
