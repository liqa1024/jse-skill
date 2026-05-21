# IFloatVectorSlicer

> `jse.math.vector.IFloatVectorSlicer`

**核心职能**：通用的 float 向量切片器，接受 List 方便抽象的切片。内部使用且半弃用，优先使用 `subVec()`。

```java
IFloatVector get(ISlice aIndices)
IFloatVector get(int[] aIndices)
IFloatVector get(List<Integer> aIndices)
IFloatVector get(SliceType aIndices)
IFloatVector get(IIndexFilter aIndices)
```
