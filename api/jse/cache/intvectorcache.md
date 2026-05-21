# IntVectorCache

> `jse.cache.IntVectorCache`

**核心职能**：专门针对 `IIntVector` / `List<IIntVector>` 的全局静态缓存，基于 `IntArrayCache`。内部 `CacheableIntVector` 继承 `IntVector`。

```java
static boolean isFromCache(IIntVector aVector)

static void returnVec(@NotNull IIntVector aVector)
static void returnVec(@NotNull List<? extends @NotNull IIntVector> aVectorList)

static @NotNull IntVector getZeros(int aSize)
static @NotNull List<IntVector> getZeros(int aSize, int aMultiple)

static @NotNull IntVector getVec(int aSize)
static @NotNull List<IntVector> getVec(int aSize, int aMultiple)
```
