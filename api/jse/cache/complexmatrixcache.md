# ComplexMatrixCache

> `jse.cache.ComplexMatrixCache`

**核心职能**：专门针对 `IComplexMatrix` / `List<IComplexMatrix>` 的全局静态缓存，基于 `DoubleArrayCache`。内部提供 `CacheableColumnComplexMatrix`（继承 `ColumnComplexMatrix`）和 `CacheableRowComplexMatrix`（继承 `RowComplexMatrix`）。支持 `asVecCol()` / `asVecRow()` 零拷贝转为 `CacheableComplexVector`。默认返回 `ColumnComplexMatrix`。

```java
static boolean isFromCache(IComplexMatrix aComplexMatrix)

// --- 归还 ---
static void returnMat(@NotNull IComplexMatrix aComplexMatrix)
static void returnMat(@NotNull List<? extends @NotNull IComplexMatrix> aComplexMatrixList)

// --- 获取零矩阵 ---
static @NotNull ColumnComplexMatrix getZeros(int aRowNum, int aColNum)  // 默认 Col（重构遗漏）
static @NotNull List<ColumnComplexMatrix> getZeros(int aRowNum, int aColNum, int aMultiple)
static @NotNull ColumnComplexMatrix getZerosCol(int aRowNum, int aColNum)
static @NotNull List<ColumnComplexMatrix> getZerosCol(int aRowNum, int aColNum, int aMultiple)
static @NotNull RowComplexMatrix getZerosRow(int aRowNum, int aColNum)
static @NotNull List<RowComplexMatrix> getZerosRow(int aRowNum, int aColNum, int aMultiple)

// --- 获取矩阵 (不保证清零) ---
static @NotNull ColumnComplexMatrix getMat(int aRowNum, int aColNum)     // 默认 Col（重构遗漏）
static @NotNull List<ColumnComplexMatrix> getMat(int aRowNum, int aColNum, int aMultiple)
static @NotNull ColumnComplexMatrix getMatCol(int aRowNum, int aColNum)
static @NotNull List<ColumnComplexMatrix> getMatCol(int aRowNum, int aColNum, int aMultiple)
static @NotNull RowComplexMatrix getMatRow(int aRowNum, int aColNum)
static @NotNull List<RowComplexMatrix> getMatRow(int aRowNum, int aColNum, int aMultiple)
```
