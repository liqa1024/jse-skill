# AbstractLogicalVectorSlicer

> `jse.math.vector.AbstractLogicalVectorSlicer`

**核心职能**：逻辑型向量的切片骨架，实现 `ILogicalVectorSlicer`。内部使用且半弃用，优先使用 `subVec()`。

```java
// === 切片 ===
final ILogicalVector get(ISlice aIndices)
final ILogicalVector get(int[] aIndices)
final ILogicalVector get(List<Integer> aIndices)
final ILogicalVector get(SliceType aIndices)
final ILogicalVector get(IIndexFilter aIndices)

// === 子类需实现 ===
protected abstract ILogicalVector getL(ISlice aIndices)
protected abstract ILogicalVector getA()
protected abstract int thisSize_()
```
