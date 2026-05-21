# DoubleArrayCache

> `jse.cache.DoubleArrayCache`

**核心职能**：专门针对 `double[]` 的全局静态缓存工具。结构与 `ByteArrayCache` 完全一致（`ThreadLocal<NavigableMap<Integer, IObjectPool<double[]>>>`），返回 ≥ 要求长度的数组。被 `VectorCache` / `MatrixCache` / `ComplexVectorCache` / `ComplexMatrixCache` 内部依赖。

```java
static void returnArray(double @NotNull[] aArray)
static double @NotNull[] getZeros(int aMinSize)
static double @NotNull[] getArray(int aMinSize)

static void returnArrayFrom(int aMultiple, IListGetter<double @NotNull[]> aArrayGetter)
static void getZerosTo(int aMinSize, int aMultiple, IListSetter<double @NotNull[]> aZerosConsumer)
static void getArrayTo(int aMinSize, int aMultiple, IListSetter<double @NotNull[]> aArrayConsumer)
```
