# AbstractComplexVectorSlicer

> `jse.math.vector.AbstractComplexVectorSlicer`

**核心职能**：复数向量的切片骨架，实现 `IComplexVectorSlicer`。内部使用且半弃用，优先使用 `subVec()`。

```java
// === 切片 ===
final IComplexVector get(ISlice aIndices)
final IComplexVector get(int[] aIndices)
final IComplexVector get(List<Integer> aIndices)
final IComplexVector get(SliceType aIndices)
final IComplexVector get(IIndexFilter aIndices)

// === 子类需实现 ===
protected abstract IComplexVector getL(ISlice aIndices)
protected abstract IComplexVector getA()
protected abstract int thisSize_()
```
