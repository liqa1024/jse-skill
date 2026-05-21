# DoubleList

> `jse.code.collection.DoubleList`

**核心职能**：以 `double[]` 为后端的动态数组，实现 `IDataShell`。`new DoubleList()` 或 `new DoubleList(int initSize)`。

```java
DoubleList() / DoubleList(int initSize)
double get(int) / void set(int, double)
void add(double) / void addZeros(int)
void ensureCapacity(int) / void trimToSize() / void clear()
void forEach(DoubleConsumer)
List<Double> asList()
Vector asVec()
Vector copy2vec()
DoubleList copy()
NDArray<double[]> numpy()
DoubleList append(double) / appendAll(IVector)
```
