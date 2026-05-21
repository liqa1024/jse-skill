# AbstractLogicalVector

> `jse.math.vector.AbstractLogicalVector`

**核心职能**：逻辑型（布尔）向量的抽象骨架，实现 `ILogicalVector`。提供迭代器、类型转换、批量填充/修改、逻辑运算（and/or/xor/not）、元素翻转、all/any/count、切片、Groovy 运算符等通用实现。继承需实现 `get`/`set`/`getAndSet`/`size`/`newZeros_`。

```java
// === Iterator ===
IBooleanIterator iterator()
IBooleanSetIterator setIterator()

// === 类型转换 ===
List<Boolean> asList()
IVector asVec()
IIntVector asIntVec()
NDArray<boolean[]> numpy()
boolean[] data()

// === ISwapper ===
void swap(int aIdx1, int aIdx2)

// === 批量修改 ===
final void fill(boolean aValue)
final void fill(ILogicalVector aVector)
final void fill(ILogicalVectorGetter aVectorGetter)
void fill(Iterable<Boolean> aList)
void fill(boolean[] aData)
final void assign(BooleanSupplier aSup)
final void forEach(IBooleanConsumer aCon)

// === 元素操作 ===
void flip(int aIdx)
boolean getAndFlip(int aIdx)
void update(int aIdx, IBooleanUnaryOperator aOpt)
boolean getAndUpdate(int aIdx, IBooleanUnaryOperator aOpt)

// === 复制与切片 ===
ILogicalVector copy()
ILogicalVector subVec(int aFromIdx, int aToIdx)
// :note: 内部使用且半弃用，优先使用 subVec()
ILogicalVectorSlicer slicer()
ILogicalVectorSlicer refSlicer()


// === 运算器 ===
ILogicalVectorOperation operation()

// === 逻辑运算（Groovy 运算符接口） ===
ILogicalVector and(boolean aRHS)
ILogicalVector or(boolean aRHS)
ILogicalVector xor(boolean aRHS)
ILogicalVector and(ILogicalVector aRHS)
ILogicalVector or(ILogicalVector aRHS)
ILogicalVector xor(ILogicalVector aRHS)
ILogicalVector not()
final void and2this(boolean aRHS)
final void or2this(boolean aRHS)
final void xor2this(boolean aRHS)
final void and2this(ILogicalVector aRHS)
final void or2this(ILogicalVector aRHS)
final void xor2this(ILogicalVector aRHS)
final void not2this()
final boolean all()
final boolean any()
final int count()

// === Groovy Operators ===
@VisibleForTesting boolean call(int aIdx)
@VisibleForTesting ILogicalVector call(ISlice aIndices)
@VisibleForTesting ILogicalVector call(List<Integer> aIndices)
@VisibleForTesting ILogicalVector call(SliceType aIndices)
@VisibleForTesting ILogicalVector call(IIndexFilter aIndices)
@VisibleForTesting ILogicalVector getAt(ISlice aIndices)
@VisibleForTesting ILogicalVector getAt(List<Integer> aIndices)
@VisibleForTesting ILogicalVector getAt(SliceType aIndices)
@VisibleForTesting ILogicalVector getAt(IIndexFilter aIndices)
@VisibleForTesting void putAt(ISlice aIndices, boolean aValue)
@VisibleForTesting void putAt(ISlice aIndices, Iterable<Boolean> aList)
@VisibleForTesting void putAt(ISlice aIndices, ILogicalVector aVector)
@VisibleForTesting void putAt(List<Integer> aIndices, boolean aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, Iterable<Boolean> aList)
@VisibleForTesting void putAt(List<Integer> aIndices, ILogicalVector aVector)
@VisibleForTesting void putAt(SliceType aIndices, boolean aValue)
@VisibleForTesting void putAt(SliceType aIndices, Iterable<Boolean> aList)
@VisibleForTesting void putAt(SliceType aIndices, ILogicalVector aVector)
@VisibleForTesting void putAt(IIndexFilter aIndices, boolean aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, Iterable<Boolean> aList)
@VisibleForTesting void putAt(IIndexFilter aIndices, ILogicalVector aVector)
@VisibleForTesting boolean getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, boolean aValue)

// === 子类需实现 ===
abstract boolean get(int aIdx)
abstract void set(int aIdx, boolean aValue)
abstract boolean getAndSet(int aIdx, boolean aValue)
abstract int size()
protected abstract ILogicalVector newZeros_(int aSize)
protected String toString_(boolean aValue)
```
