# AbstractMatrixSlicer

> `jse.math.matrix.AbstractMatrixSlicer`

**核心职能**：内部使用且半弃用，优先使用 `row/col(int)`。`abstract class implements IMatrixSlicer`。矩阵切片骨架实现，通过 `public final` 方法将 35+ 种 `get()` 组合（6 种行选择器 × 5 种列选择器）派发至 8 个 `protected abstract` 方法供子类实现。

```java
// === 常量 ===
final static String COL_MSG = "SelectedCols Must be a Filter or ISlice or int[] or List<Integer> or ALL"
final static String ROW_MSG = "SelectedRows Must be a Filter or ISlice or int[] or List<Integer> or ALL"

// === 最终派发方法（全部为 public final） ===

// (ISlice|int[]|List<Integer>) × (ISlice|int[]|List<Integer>) → getLL → IMatrix
final IMatrix get(ISlice aSelectedRows, ISlice aSelectedCols)
final IMatrix get(ISlice aSelectedRows, int[] aSelectedCols)
final IMatrix get(ISlice aSelectedRows, List<Integer> aSelectedCols)
final IMatrix get(int[] aSelectedRows, ISlice aSelectedCols)
final IMatrix get(int[] aSelectedRows, int[] aSelectedCols)
final IMatrix get(int[] aSelectedRows, List<Integer> aSelectedCols)
final IMatrix get(List<Integer> aSelectedRows, ISlice aSelectedCols)
final IMatrix get(List<Integer> aSelectedRows, int[] aSelectedCols)
final IMatrix get(List<Integer> aSelectedRows, List<Integer> aSelectedCols)

// (ISlice|int[]|List<Integer>) × ALL → getLA → IMatrix
final IMatrix get(ISlice aSelectedRows, SliceType aSelectedCols)
final IMatrix get(int[] aSelectedRows, SliceType aSelectedCols)
final IMatrix get(List<Integer> aSelectedRows, SliceType aSelectedCols)

// ALL × (ISlice|int[]|List<Integer>) → getAL → IMatrix
final IMatrix get(SliceType aSelectedRows, ISlice aSelectedCols)
final IMatrix get(SliceType aSelectedRows, int[] aSelectedCols)
final IMatrix get(SliceType aSelectedRows, List<Integer> aSelectedCols)

// ALL × ALL → getAA → IMatrix
final IMatrix get(SliceType aSelectedRows, SliceType aSelectedCols)

// int × (ISlice|int[]|List<Integer>) → getIL → IVector
final IVector get(int aSelectedRow, ISlice aSelectedCols)
final IVector get(int aSelectedRow, int[] aSelectedCols)
final IVector get(int aSelectedRow, List<Integer> aSelectedCols)

// int × ALL → getIA → IVector
final IVector get(int aSelectedRow, SliceType aSelectedCols)

// (ISlice|int[]|List<Integer>) × int → getLI → IVector
final IVector get(ISlice aSelectedRows, int aSelectedCol)
final IVector get(int[] aSelectedRows, int aSelectedCol)
final IVector get(List<Integer> aSelectedRows, int aSelectedCol)

// ALL × int → getAI → IVector
final IVector get(SliceType aSelectedRows, int aSelectedCol)

// IIndexFilter 变体（先经 NewCollections.filterInt 转换为 int[] 再派发）
final IMatrix get(IIndexFilter aSelectedRows, ISlice aSelectedCols)
final IMatrix get(IIndexFilter aSelectedRows, int[] aSelectedCols)
final IMatrix get(IIndexFilter aSelectedRows, List<Integer> aSelectedCols)
final IMatrix get(IIndexFilter aSelectedRows, SliceType aSelectedCols)
final IMatrix get(ISlice aSelectedRows, IIndexFilter aSelectedCols)
final IMatrix get(int[] aSelectedRows, IIndexFilter aSelectedCols)
final IMatrix get(List<Integer> aSelectedRows, IIndexFilter aSelectedCols)
final IMatrix get(SliceType aSelectedRows, IIndexFilter aSelectedCols)
final IMatrix get(IIndexFilter aSelectedRows, IIndexFilter aSelectedCols)
final IVector get(int aSelectedRow, IIndexFilter aSelectedCols)
final IVector get(IIndexFilter aSelectedRows, int aSelectedCol)

// 对角线（零偏移，委派至 diag(int)）
final IVector diag()

// === 需子类实现的抽象方法 ===
// 行/列向量切片
protected abstract IVector getIL(int aSelectedRow, ISlice aSelectedCols)
protected abstract IVector getLI(ISlice aSelectedRows, int aSelectedCol)
protected abstract IVector getIA(int aSelectedRow)
protected abstract IVector getAI(int aSelectedCol)

// 子矩阵切片
protected abstract IMatrix getLL(ISlice aSelectedRows, ISlice aSelectedCols)
protected abstract IMatrix getLA(ISlice aSelectedRows)
protected abstract IMatrix getAL(ISlice aSelectedCols)
protected abstract IMatrix getAA()

// 对角线（含偏移量）
abstract IVector diag(int aShift)

// === 维度辅助 ===
protected abstract int thisNRows_()
protected abstract int thisNCols_()
```
