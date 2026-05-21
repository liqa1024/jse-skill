# IIntVectorSlicer

> `jse.math.vector.IIntVectorSlicer`

**核心职能**：通用的 int 向量切片器，接受 List 方便抽象的切片。内部使用且半弃用，优先使用 `subVec()`。

```java
IIntVector get(ISlice aIndices)
IIntVector get(int[] aIndices)
IIntVector get(List<Integer> aIndices)
IIntVector get(SliceType aIndices)
IIntVector get(IIndexFilter aIndices)
```
