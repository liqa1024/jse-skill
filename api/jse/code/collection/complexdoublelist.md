# ComplexDoubleList

> `jse.code.collection.ComplexDoubleList`

**核心职能**：以 `double[2][]`（实部+虚部成对存储）为后端的复数动态数组，实现 `IDataShell`。`new ComplexDoubleList()` 或 `new ComplexDoubleList(int initSize)`。

```java
ComplexDoubleList() / ComplexDoubleList(int initSize)
double getReal(int) / double getImag(int)
void setReal(int, double) / void setImag(int, double)
void set(int, double, double) / void get(int, IComplexDouble)
void add(double, double) / void addZeros(int)
void ensureCapacity(int) / void trimToSize() / void clear()
void forEach(Consumer<IComplexDouble>)
List<IComplexDouble> asList()
ComplexVector asVec()
ComplexVector copy2vec()
ComplexDoubleList copy()
NDArray<double[]> numpy()
ComplexDoubleList append(double, double) / appendAll(IComplexVector)
```
