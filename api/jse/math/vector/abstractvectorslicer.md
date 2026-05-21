# AbstractVectorSlicer

> `jse.math.vector.AbstractVectorSlicer`

**核心职能**：`implements IVectorSlicer`。内部使用且半弃用，优先使用 `subVec()`。骨架实现：各种参数类型的 `get()` `final` 方法均转发至两个受保护抽象方法，子类只需实现 `getL(ISlice)`、`getA()`、`thisSize_()`。

```java
// === 具体 get 方法（final，统一转发至 getL / getA） ===
final IVector get(ISlice aIndices)
final IVector get(int[] aIndices)
final IVector get(List<Integer> aIndices)
final IVector get(SliceType aIndices)
final IVector get(IIndexFilter aIndices)

// === 抽象方法（子类须实现） ===
protected abstract IVector getL(ISlice aIndices)
protected abstract IVector getA()
protected abstract int thisSize_()
```
