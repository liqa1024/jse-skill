# IMatrixSlicer

> `jse.math.matrix.IMatrixSlicer`

**核心职能**：内部使用且半弃用，优先使用 `row/col(int)`。矩阵切片接口，提供 5 种行选择器 × 5 种列选择器的组合式 `get()` 重载，以及 `diag()` 对角线提取。

```java
// === 行选择器 ISlice × 列选择器 ===
IMatrix get(ISlice aSelectedRows, ISlice aSelectedCols)
IMatrix get(ISlice aSelectedRows, int[] aSelectedCols)
IMatrix get(ISlice aSelectedRows, List<Integer> aSelectedCols)
IMatrix get(ISlice aSelectedRows, SliceType aSelectedCols)
IMatrix get(ISlice aSelectedRows, IIndexFilter aSelectedCols)

// === 行选择器 int[] × 列选择器 ===
IMatrix get(int[] aSelectedRows, ISlice aSelectedCols)
IMatrix get(int[] aSelectedRows, int[] aSelectedCols)
IMatrix get(int[] aSelectedRows, List<Integer> aSelectedCols)
IMatrix get(int[] aSelectedRows, SliceType aSelectedCols)
IMatrix get(int[] aSelectedRows, IIndexFilter aSelectedCols)

// === 行选择器 List<Integer> × 列选择器 ===
IMatrix get(List<Integer> aSelectedRows, ISlice aSelectedCols)
IMatrix get(List<Integer> aSelectedRows, int[] aSelectedCols)
IMatrix get(List<Integer> aSelectedRows, List<Integer> aSelectedCols)
IMatrix get(List<Integer> aSelectedRows, SliceType aSelectedCols)
IMatrix get(List<Integer> aSelectedRows, IIndexFilter aSelectedCols)

// === 行选择器 SliceType × 列选择器 ===
IMatrix get(SliceType aSelectedRows, ISlice aSelectedCols)
IMatrix get(SliceType aSelectedRows, int[] aSelectedCols)
IMatrix get(SliceType aSelectedRows, List<Integer> aSelectedCols)
IMatrix get(SliceType aSelectedRows, SliceType aSelectedCols)
IMatrix get(SliceType aSelectedRows, IIndexFilter aSelectedCols)

// === 行选择器 IIndexFilter × 列选择器 ===
IMatrix get(IIndexFilter aSelectedRows, ISlice aSelectedCols)
IMatrix get(IIndexFilter aSelectedRows, int[] aSelectedCols)
IMatrix get(IIndexFilter aSelectedRows, List<Integer> aSelectedCols)
IMatrix get(IIndexFilter aSelectedRows, SliceType aSelectedCols)
IMatrix get(IIndexFilter aSelectedRows, IIndexFilter aSelectedCols)

// === 单行 × 列选择器 ===
IVector get(int aSelectedRow, ISlice aSelectedCols)
IVector get(int aSelectedRow, int[] aSelectedCols)
IVector get(int aSelectedRow, List<Integer> aSelectedCols)
IVector get(int aSelectedRow, SliceType aSelectedCols)
IVector get(int aSelectedRow, IIndexFilter aSelectedCols)

// === 行选择器 × 单列 ===
IVector get(ISlice aSelectedRows, int aSelectedCol)
IVector get(int[] aSelectedRows, int aSelectedCol)
IVector get(List<Integer> aSelectedRows, int aSelectedCol)
IVector get(SliceType aSelectedRows, int aSelectedCol)
IVector get(IIndexFilter aSelectedRows, int aSelectedCol)

// === 对角线 ===
IVector diag()
IVector diag(int aShift)
```
