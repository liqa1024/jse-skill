# AbstractLongVector

> `jse.math.vector.AbstractLongVector`

**核心职能**：长整型向量的抽象骨架，实现 `ILongVector`。提供迭代器、类型转换、批量填充/修改、元素增减、切片、Groovy 运算符等通用实现。继承需实现 `get`/`set`/`getAndSet`/`size`/`newZeros_`。

```java
// === Iterator ===
ILongIterator iterator()
ILongSetIterator setIterator()

// === 类型转换 ===
List<Long> asList()
IVector asVec()
IIntVector asIntVec()
NDArray<long[]> numpy()
long[] data()

// === ISwapper ===
void swap(int aIdx1, int aIdx2)

// === 批量修改 ===
final void fill(long aValue)
final void fill(ILongVector aVector)
final void fill(ILongVectorGetter aVectorGetter)
void fill(Iterable<? extends Number> aList)
void fill(long[] aData)
final void assign(LongSupplier aSup)
final void forEach(LongConsumer aCon)

// === 元素操作 ===
void increment(int aIdx)
long getAndIncrement(int aIdx)
void decrement(int aIdx)
long getAndDecrement(int aIdx)
void add(int aIdx, long aDelta)
long getAndAdd(int aIdx, long aDelta)
void update(int aIdx, LongUnaryOperator aOpt)
long getAndUpdate(int aIdx, LongUnaryOperator aOpt)

// === 复制与切片 ===
ILongVector copy()
ILongVector subVec(int aFromIdx, int aToIdx)
// :note: 内部使用且半弃用，优先使用 subVec()
ILongVectorSlicer slicer()
ILongVectorSlicer refSlicer()


// === 运算器 ===
ILongVectorOperation operation()

// === 统计与排序 ===
final long sum()
final double mean()
final double prod()
final long max()
final long min()
final void sort()

// === Groovy Operators ===
@VisibleForTesting long call(int aIdx)
@VisibleForTesting ILongVector call(ISlice aIndices)
@VisibleForTesting ILongVector call(List<Integer> aIndices)
@VisibleForTesting ILongVector call(SliceType aIndices)
@VisibleForTesting ILongVector call(IIndexFilter aIndices)
@VisibleForTesting ILongVector getAt(ISlice aIndices)
@VisibleForTesting ILongVector getAt(List<Integer> aIndices)
@VisibleForTesting ILongVector getAt(SliceType aIndices)
@VisibleForTesting ILongVector getAt(IIndexFilter aIndices)
@VisibleForTesting void putAt(ISlice aIndices, long aValue)
@VisibleForTesting void putAt(ISlice aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(ISlice aIndices, ILongVector aVector)
@VisibleForTesting void putAt(List<Integer> aIndices, long aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(List<Integer> aIndices, ILongVector aVector)
@VisibleForTesting void putAt(SliceType aIndices, long aValue)
@VisibleForTesting void putAt(SliceType aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(SliceType aIndices, ILongVector aVector)
@VisibleForTesting void putAt(IIndexFilter aIndices, long aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(IIndexFilter aIndices, ILongVector aVector)
@VisibleForTesting long getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, long aValue)

// === 子类需实现 ===
abstract long get(int aIdx)
abstract void set(int aIdx, long aValue)
abstract long getAndSet(int aIdx, long aValue)
abstract int size()
protected abstract ILongVector newZeros_(int aSize)
protected String toString_(long aValue)
```
