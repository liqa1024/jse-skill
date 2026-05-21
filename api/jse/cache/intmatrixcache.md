# IntMatrixCache

> `jse.cache.IntMatrixCache`

**核心职能**：专门针对 `IIntMatrix` / `List<IIntMatrix>` 的全局静态缓存，基于 `IntArrayCache`。内部提供 `CacheableColumnIntMatrix`（继承 `ColumnIntMatrix`）和 `CacheableRowIntMatrix`（继承 `RowIntMatrix`）。默认返回 `ColumnIntMatrix`。

```java
// --- 来源检测 (package-private) ---
static boolean isFromCache(IIntMatrix aIntMatrix)

// --- 归还 ---
static void returnMat(@NotNull IIntMatrix aMatrix)
static void returnMat(@NotNull List<? extends @NotNull IIntMatrix> aMatrixList)

// --- 获取零矩阵 ---
static @NotNull ColumnIntMatrix getZeros(int aRowNum, int aColNum)   // 默认 Col（重构遗漏）
static @NotNull List<ColumnIntMatrix> getZeros(int aRowNum, int aColNum, int aMultiple)
static @NotNull ColumnIntMatrix getZerosCol(int aRowNum, int aColNum)
static @NotNull List<ColumnIntMatrix> getZerosCol(int aRowNum, int aColNum, int aMultiple)
static @NotNull RowIntMatrix getZerosRow(int aRowNum, int aColNum)
static @NotNull List<RowIntMatrix> getZerosRow(int aRowNum, int aColNum, int aMultiple)

// --- 获取矩阵 (不保证清零) ---
static @NotNull ColumnIntMatrix getMat(int aRowNum, int aColNum)     // 默认 Col（重构遗漏）
static @NotNull List<ColumnIntMatrix> getMat(int aRowNum, int aColNum, int aMultiple)
static @NotNull ColumnIntMatrix getMatCol(int aRowNum, int aColNum)
static @NotNull List<ColumnIntMatrix> getMatCol(int aRowNum, int aColNum, int aMultiple)
static @NotNull RowIntMatrix getMatRow(int aRowNum, int aColNum)
static @NotNull List<RowIntMatrix> getMatRow(int aRowNum, int aColNum, int aMultiple)
```
