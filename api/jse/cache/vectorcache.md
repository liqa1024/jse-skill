# VectorCache

> `jse.cache.VectorCache`

**核心职能**：专门针对 `IVector` / `List<IVector>` 的全局静态缓存工具，基于 `DoubleArrayCache` 实现。内部使用 `CacheableVector`（继承 `Vector` + 实现 `ICacheableVector`）包装缓存数据——从缓存获取的 Vector **禁止后续 setInternalData**（抛出 `UnsupportedOperationException`）。

```java
// --- 来源检测 ---
static boolean isFromCache(IVector aVector)

// --- 归还 ---
static void returnVec(@NotNull IVector aVector)                      // 单个归还（非缓存来源抛异常）
static void returnVec(@NotNull List<? extends @NotNull IVector> aVectorList)  // 批量归还（逐元素提取 double[] 统一归还）

// --- 获取零向量 ---
static @NotNull Vector getZeros(int aSize)                           // 单个全零 Vector
static @NotNull List<Vector> getZeros(int aSize, int aMultiple)      // 批量全零 Vector

// --- 获取向量 (不保证清零) ---
static @NotNull Vector getVec(int aSize)
static @NotNull List<Vector> getVec(int aSize, int aMultiple)
```
