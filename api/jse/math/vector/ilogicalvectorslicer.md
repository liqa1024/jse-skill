# ILogicalVectorSlicer

> `jse.math.vector.ILogicalVectorSlicer`

**核心职能**：通用的 boolean 向量切片器，接受 List 方便抽象的切片。内部使用且半弃用，优先使用 `subVec()`。

```java
ILogicalVector get(ISlice aIndices)
ILogicalVector get(int[] aIndices)
ILogicalVector get(List<Integer> aIndices)
ILogicalVector get(SliceType aIndices)
ILogicalVector get(IIndexFilter aIndices)
```
