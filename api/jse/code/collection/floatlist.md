# FloatList

> `jse.code.collection.FloatList`

**核心职能**：以 `float[]` 为后端的动态数组，实现 `IDataShell`。`new FloatList()` 或 `new FloatList(int initSize)`。

```java
FloatList() / FloatList(int initSize)
float get(int) / void set(int, float)
void add(float) / void addZeros(int)
void ensureCapacity(int) / void trimToSize() / void clear()
void forEach(FloatConsumer)
List<Float> asList()
FloatVector asVec()
FloatVector copy2vec()
FloatList copy()
NDArray<float[]> numpy()
FloatList append(float) / appendAll(IFloatVector)
```
