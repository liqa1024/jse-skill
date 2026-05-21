# FloatVectorCache

> `jse.cache.FloatVectorCache`

**核心职能**：专门针对 `IFloatVector` / `List<IFloatVector>` 的全局静态缓存，基于 `FloatArrayCache`。结构同 `VectorCache`——内部 `CacheableFloatVector` 继承 `FloatVector`，禁止 setInternalData。

```java
static boolean isFromCache(IFloatVector aVector)

static void returnVec(@NotNull IFloatVector aVector)
static void returnVec(@NotNull List<? extends @NotNull IFloatVector> aVectorList)

static @NotNull FloatVector getZeros(int aSize)
static @NotNull List<FloatVector> getZeros(int aSize, int aMultiple)

static @NotNull FloatVector getVec(int aSize)
static @NotNull List<FloatVector> getVec(int aSize, int aMultiple)
```
