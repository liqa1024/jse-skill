# MatrixCache

> `jse.cache.MatrixCache`

**核心职能**：专门针对 `IMatrix` / `List<IMatrix>` 的全局静态缓存工具，基于 `DoubleArrayCache` 实现。内部提供 `CacheableColumnMatrix`（继承 `ColumnMatrix`）和 `CacheableRowMatrix`（继承 `RowMatrix`）两种包装。支持 `asVecCol()` / `asVecRow()` 零拷贝转换为 `CacheableVector`。默认 `getZeros` / `getMat` 返回 `RowMatrix`；后缀 `Col` / `Row` 精确指定。

```java
// --- 来源检测 ---
static boolean isFromCache(IMatrix aMatrix)

// --- 归还 ---
static void returnMat(@NotNull IMatrix aMatrix)
static void returnMat(@NotNull List<? extends @NotNull IMatrix> aMatrixList)

// --- 获取零矩阵 ---
static @NotNull RowMatrix getZeros(int aNumRows, int aNumCols)      // 默认 Row
static @NotNull List<RowMatrix> getZeros(int aNumRows, int aNumCols, int aMultiple)
static @NotNull ColumnMatrix getZerosCol(int aNumRows, int aNumCols)
static @NotNull List<ColumnMatrix> getZerosCol(int aNumRows, int aNumCols, int aMultiple)
static @NotNull RowMatrix getZerosRow(int aNumRows, int aNumCols)
static @NotNull List<RowMatrix> getZerosRow(int aNumRows, int aNumCols, int aMultiple)

// --- 获取矩阵 (不保证清零) ---
static @NotNull RowMatrix getMat(int aNumRows, int aNumCols)         // 默认 Row
static @NotNull List<RowMatrix> getMat(int aNumRows, int aNumCols, int aMultiple)
static @NotNull ColumnMatrix getMatCol(int aNumRows, int aNumCols)
static @NotNull List<ColumnMatrix> getMatCol(int aNumRows, int aNumCols, int aMultiple)
static @NotNull RowMatrix getMatRow(int aNumRows, int aNumCols)
static @NotNull List<RowMatrix> getMatRow(int aNumRows, int aNumCols, int aMultiple)
```
