# AbstractIntVectorSlicer

> `jse.math.vector.AbstractIntVectorSlicer`

**核心职能**：`implements IIntVectorSlicer`。内部使用且半弃用，优先使用 `subVec()`。骨架实现：各种参数类型的 `get()` `final` 方法均转发至两个受保护抽象方法，子类只需实现 `getL(ISlice)`、`getA()`、`thisSize_()`。

```java
// === 具体 get 方法（final，统一转发至 getL / getA） ===
final IIntVector get(ISlice aIndices)
final IIntVector get(int[] aIndices)
final IIntVector get(List<Integer> aIndices)
final IIntVector get(SliceType aIndices)
final IIntVector get(IIndexFilter aIndices)

// === 抽象方法（子类须实现） ===
protected abstract IIntVector getL(ISlice aIndices)
protected abstract IIntVector getA()
protected abstract int thisSize_()
```
