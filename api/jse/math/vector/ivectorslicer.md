# IVectorSlicer

> `jse.math.vector.IVectorSlicer`

**核心职能**：内部使用且半弃用，优先使用 `subVec()`。基于多种索引选择器获取向量切片。

```java
IVector get(ISlice aIndices)
IVector get(int[] aIndices)
IVector get(List<Integer> aIndices)
IVector get(SliceType aIndices)
IVector get(IIndexFilter aIndices)
```
