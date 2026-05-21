# ComplexVectorCache

> `jse.cache.ComplexVectorCache`

**核心职能**：专门针对 `IComplexVector` / `List<IComplexVector>` 的全局静态缓存，基于 `DoubleArrayCache`。内存结构为 `double[2][]`（实部+虚部两个独立 `double[]`），分别作为独立缓存条目管理。内部 `CacheableComplexVector` 继承 `ComplexVector`。

```java
static boolean isFromCache(IComplexVector aVector)

static void returnVec(@NotNull IComplexVector aComplexVector)
static void returnVec(@NotNull List<? extends @NotNull IComplexVector> aComplexVectorList)

static @NotNull ComplexVector getZeros(int aSize)
static @NotNull List<ComplexVector> getZeros(int aSize, int aMultiple)

static @NotNull ComplexVector getVec(int aSize)
static @NotNull List<ComplexVector> getVec(int aSize, int aMultiple)
```
