# AbstractLongVectorSlicer

> `jse.math.vector.AbstractLongVectorSlicer`

**核心职能**：长整型向量的切片骨架，实现 `ILongVectorSlicer`。内部使用且半弃用，优先使用 `subVec()`。

```java
// === 切片 ===
final ILongVector get(ISlice aIndices)
final ILongVector get(int[] aIndices)
final ILongVector get(List<Integer> aIndices)
final ILongVector get(SliceType aIndices)
final ILongVector get(IIndexFilter aIndices)

// === 子类需实现 ===
protected abstract ILongVector getL(ISlice aIndices)
protected abstract ILongVector getA()
protected abstract int thisSize_()
```
