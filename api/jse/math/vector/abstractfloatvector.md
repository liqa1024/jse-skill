# AbstractFloatVector

> `jse.math.vector.AbstractFloatVector`

**核心职能**：`implements IFloatVector`。float 类型向量的骨架实现，无算术/统计（float 类型不提供）。提供迭代器、转换视图、批量填充/赋值/遍历、单元素 update、切片 (subVec/slicer)、Groovy 运算符重载。算术/统计操作通过 `asVec()` 获取 double 引用视图后转入 `IVector` 主线。子类只需实现 5 个抽象方法。

```java
// === 抽象方法（子类须实现） ===
abstract int size()
abstract float get(int aIdx)
abstract void set(int aIdx, float aValue)
abstract float getAndSet(int aIdx, float aValue)
protected abstract IFloatVector newZeros_(int aSize)

// === 迭代器 ===
IFloatIterator iterator()
IFloatSetIterator setIterator()

// === 转换 / 视图 ===
List<Float> asList()
IVector asVec()
NDArray<float[]> numpy()
float[] data()

// === ISwapper ===
void swap(int aIdx1, int aIdx2)

// === 批量填充 / 赋值 / 遍历（通过 operation() 转发） ===
final void fill(float aValue)
final void fill(IFloatVector aVector)
final void fill(IFloatVectorGetter aVectorGetter)
final void fill(Iterable<? extends Number> aList)
void fill(float[] aData)
final void assign(IFloatSupplier aSup)
final void forEach(IFloatConsumer aCon)

// === 单元素操作 ===
void update(int aIdx, IFloatUnaryOperator aOpt)
float getAndUpdate(int aIdx, IFloatUnaryOperator aOpt)

// === 切片 ===
IFloatVector copy()
IFloatVector subVec(int aFromIdx, int aToIdx)
// :note: 内部使用且半弃用，优先使用 subVec()
IFloatVectorSlicer slicer()
IFloatVectorSlicer refSlicer()


// === 运算器 ===
IFloatVectorOperation operation()

// :note: Groovy 脚本优先使用 v[i] / v[i] = x 运算符访问
// === Groovy 运算符重载 `[]`（@VisibleForTesting） ===
@VisibleForTesting float call(int aIdx)
@VisibleForTesting IFloatVector call(ISlice aIndices)
@VisibleForTesting IFloatVector call(List<Integer> aIndices)
@VisibleForTesting IFloatVector call(SliceType aIndices)
@VisibleForTesting IFloatVector call(IIndexFilter aIndices)
@VisibleForTesting IFloatVector getAt(ISlice aIndices)
@VisibleForTesting IFloatVector getAt(List<Integer> aIndices)
@VisibleForTesting IFloatVector getAt(SliceType aIndices)
@VisibleForTesting IFloatVector getAt(IIndexFilter aIndices)
@VisibleForTesting void putAt(ISlice aIndices, float aValue)
@VisibleForTesting void putAt(ISlice aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(ISlice aIndices, IFloatVector aVector)
@VisibleForTesting void putAt(List<Integer> aIndices, float aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(List<Integer> aIndices, IFloatVector aVector)
@VisibleForTesting void putAt(SliceType aIndices, float aValue)
@VisibleForTesting void putAt(SliceType aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(SliceType aIndices, IFloatVector aVector)
@VisibleForTesting void putAt(IIndexFilter aIndices, float aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(IIndexFilter aIndices, IFloatVector aVector)
@VisibleForTesting float getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, float aValue)

// === 辅助（protected，子类可覆写显示格式） ===
protected String toString_(float aValue)
```
