# LogicalVectorCache

> `jse.cache.LogicalVectorCache`

**核心职能**：专门针对 `ILogicalVector` / `List<ILogicalVector>` 的全局静态缓存，基于 `BooleanArrayCache`。内部 `CacheableLogicalVector` 继承 `LogicalVector`。

```java
// --- 来源检测 (package-private) ---
static boolean isFromCache(ILogicalVector aVector)

// --- 归还 ---
static void returnVec(@NotNull ILogicalVector aVector)
static void returnVec(@NotNull List<? extends @NotNull ILogicalVector> aVectorList)

// --- 获取 ---
static @NotNull LogicalVector getZeros(int aSize)
static @NotNull List<LogicalVector> getZeros(int aSize, int aMultiple)

static @NotNull LogicalVector getVec(int aSize)
static @NotNull List<LogicalVector> getVec(int aSize, int aMultiple)
```
