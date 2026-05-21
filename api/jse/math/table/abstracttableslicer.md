# AbstractTableSlicer

> `jse.math.table.AbstractTableSlicer`

**核心职能**：`abstract class implements ITableSlicer`。实现组合式切片分派：所有 `final` 的 `get()` 重载（~30 个，6 种行选择器 × 5 种列选择器）委托到 4 个 protected abstract 方法（`getLL`/`getLA`/`getAL`/`getAA`）完成实际切片。

```java
// === 行选择器 × 列选择器（全部 final 分派） ===
// 行选择器类型：ISlice / int[] / List<Integer> / SliceType / int / IIndexFilter
// 列选择器类型：String[] / String / SliceType / Iterable<? extends CharSequence> / IFilter<String>
ITable get(ISlice aSelectedRows, String[] aSelectedCols)
ITable get(ISlice aSelectedRows, String aSelectedCol)
ITable get(ISlice aSelectedRows, SliceType aSelectedCols)
ITable get(ISlice aSelectedRows, IFilter<String> aSelectedCols)
ITable get(ISlice aSelectedRows, Iterable<? extends CharSequence> aSelectedCols)
ITable get(int[] aSelectedRows, String[] aSelectedCols)
ITable get(int[] aSelectedRows, String aSelectedCol)
ITable get(int[] aSelectedRows, SliceType aSelectedCols)
ITable get(int[] aSelectedRows, IFilter<String> aSelectedCols)
ITable get(int[] aSelectedRows, Iterable<? extends CharSequence> aSelectedCols)
ITable get(List<Integer> aSelectedRows, String[] aSelectedCols)
ITable get(List<Integer> aSelectedRows, String aSelectedCol)
ITable get(List<Integer> aSelectedRows, SliceType aSelectedCols)
ITable get(List<Integer> aSelectedRows, IFilter<String> aSelectedCols)
ITable get(List<Integer> aSelectedRows, Iterable<? extends CharSequence> aSelectedCols)
ITable get(SliceType aSelectedRows, String[] aSelectedCols)
ITable get(SliceType aSelectedRows, String aSelectedCol)
ITable get(SliceType aSelectedRows, SliceType aSelectedCols)
ITable get(SliceType aSelectedRows, IFilter<String> aSelectedCols)
ITable get(SliceType aSelectedRows, Iterable<? extends CharSequence> aSelectedCols)
ITable get(int aSelectedRow, String[] aSelectedCols)
ITable get(int aSelectedRow, String aSelectedCol)
ITable get(int aSelectedRow, SliceType aSelectedCols)
ITable get(int aSelectedRow, IFilter<String> aSelectedCols)
ITable get(int aSelectedRow, Iterable<? extends CharSequence> aSelectedCols)
ITable get(IIndexFilter aSelectedRows, String[] aSelectedCols)
ITable get(IIndexFilter aSelectedRows, String aSelectedCol)
ITable get(IIndexFilter aSelectedRows, SliceType aSelectedCols)
ITable get(IIndexFilter aSelectedRows, IFilter<String> aSelectedCols)
ITable get(IIndexFilter aSelectedRows, Iterable<? extends CharSequence> aSelectedCols)

// === protected abstract 分派目标（子类覆写） ===
protected abstract ITable getLL(ISlice aSelectedRows, ISlice aSelectedCols)
protected abstract ITable getLA(ISlice aSelectedRows)
protected abstract ITable getAL(ISlice aSelectedCols)
protected abstract ITable getAA()
protected abstract int thisRowNum_()
protected abstract int head2col_(String aHead)
protected abstract Iterable<String> thisHeads_()
```
