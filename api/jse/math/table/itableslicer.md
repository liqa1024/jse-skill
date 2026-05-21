# ITableSlicer

> `jse.math.table.ITableSlicer`

**核心职能**：支持 31 种行列组合切片——行用 `ISlice/int[]/List/SliceType/IIndexFilter/int`，列用 `String[]/String/SliceType/IFilter<String>/Iterable<CharSequence>`。

```java
ITable get(ISlice/int[]/List<Integer>/SliceType/IIndexFilter/int rows,
           String[]/String/SliceType/IFilter<String>/Iterable<CharSequence> cols)
// 5 种行选择器 × 5 种列选择器 + IIndexFilter 行变体 + IFilter<String> 列变体 = 31 种组合
```
