# IComplexVectorSlicer

> `jse.math.vector.IComplexVectorSlicer`

**核心职能**：通用的复数向量切片器，接受 List 方便抽象的切片。内部使用且半弃用，优先使用 `subVec()`。

```java
IComplexVector get(ISlice aIndices)
IComplexVector get(int[] aIndices)
IComplexVector get(List<Integer> aIndices)
IComplexVector get(SliceType aIndices)
IComplexVector get(IIndexFilter aIndices)
```
