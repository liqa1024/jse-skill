# ILongVectorSlicer

> `jse.math.vector.ILongVectorSlicer`

**核心职能**：通用的 long 向量切片器，接受 List 方便抽象的切片。内部使用且半弃用，优先使用 `subVec()`。

```java
ILongVector get(ISlice aIndices)
ILongVector get(int[] aIndices)
ILongVector get(List<Integer> aIndices)
ILongVector get(SliceType aIndices)
ILongVector get(IIndexFilter aIndices)
```
