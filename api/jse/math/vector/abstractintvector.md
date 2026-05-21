# AbstractIntVector

> `jse.math.vector.AbstractIntVector`

**核心职能**：`implements IIntVector`。int 类型向量的骨架实现。提供全部接口方法的默认行为 — 迭代器、转换视图、批量填充/赋值/遍历、单元素原子操作 (increment/decrement/add/update)、切片 (subVec/slicer)、Groovy 运算符重载；算术/统计/sort/shuffle 通过 `operation()` 转发至 `IIntVectorOperation`，均声明 `final`。子类只需实现 5 个抽象方法。

```java
// === 抽象方法（子类须实现） ===
abstract int size()
abstract int get(int aIdx)
abstract void set(int aIdx, int aValue)
abstract int getAndSet(int aIdx, int aValue)
protected abstract IIntVector newZeros_(int aSize)

// === 迭代器 ===
IIntIterator iterator()
IIntSetIterator setIterator()

// === 转换 / 视图 ===
List<Integer> asList()
IVector asVec()
NDArray<int[]> numpy()
int[] data()

// === ISwapper ===
void swap(int aIdx1, int aIdx2)

// === 批量填充 / 赋值 / 遍历（通过 operation() 转发） ===
final void fill(int aValue)
final void fill(IIntVector aVector)
final void fill(IIntVectorGetter aVectorGetter)
final void fill(Iterable<? extends Number> aList)
void fill(int[] aData)
final void assign(IntSupplier aSup)
final void forEach(IntConsumer aCon)

// === 单元素原子操作 ===
void increment(int aIdx)
int getAndIncrement(int aIdx)
void decrement(int aIdx)
int getAndDecrement(int aIdx)
void add(int aIdx, int aDelta)
int getAndAdd(int aIdx, int aDelta)
void update(int aIdx, IntUnaryOperator aOpt)
int getAndUpdate(int aIdx, IntUnaryOperator aOpt)

// === 切片 ===
IIntVector copy()
IIntVector subVec(int aFromIdx, int aToIdx)
// :note: 内部使用且半弃用，优先使用 subVec()
IIntVectorSlicer slicer()
IIntVectorSlicer refSlicer()


// === 运算器 ===
IIntVectorOperation operation()

// === 标量算术（new IIntVector，通过 operation()，final） ===
final IIntVector plus(int aRHS)
final IIntVector minus(int aRHS)
final IIntVector multiply(int aRHS)
final IIntVector div(int aRHS)
final IIntVector mod(int aRHS)

// === 向量逐元素算术（new IIntVector，通过 operation()，final） ===
final IIntVector plus(IIntVector aRHS)
final IIntVector minus(IIntVector aRHS)
final IIntVector multiply(IIntVector aRHS)
final IIntVector div(IIntVector aRHS)
final IIntVector mod(IIntVector aRHS)

// === 原位运算 2this（通过 operation()，final） ===
final void plus2this(int aRHS)
final void minus2this(int aRHS)
final void multiply2this(int aRHS)
final void div2this(int aRHS)
final void mod2this(int aRHS)
final void plus2this(IIntVector aRHS)
final void minus2this(IIntVector aRHS)
final void multiply2this(IIntVector aRHS)
final void div2this(IIntVector aRHS)
final void mod2this(IIntVector aRHS)

// === 一元运算 ===
final IIntVector abs()
final void abs2this()
final IIntVector negative()
final void negative2this()

// === 统计归约 ===
final int sum()
final double mean()
final double prod()
final int max()
final int min()
final void sort()

// === 排序 / 乱序 ===
final void shuffle()
final void shuffle(IRandom aRng)

// :note: Groovy 脚本优先使用 v[i] / v[i] = x 运算符访问
// === Groovy 运算符重载 `[]`（@VisibleForTesting） ===
@VisibleForTesting int call(int aIdx)
@VisibleForTesting IIntVector call(ISlice aIndices)
@VisibleForTesting IIntVector call(List<Integer> aIndices)
@VisibleForTesting IIntVector call(SliceType aIndices)
@VisibleForTesting IIntVector call(IIndexFilter aIndices)
@VisibleForTesting IIntVector getAt(ISlice aIndices)
@VisibleForTesting IIntVector getAt(List<Integer> aIndices)
@VisibleForTesting IIntVector getAt(SliceType aIndices)
@VisibleForTesting IIntVector getAt(IIndexFilter aIndices)
@VisibleForTesting void putAt(ISlice aIndices, int aValue)
@VisibleForTesting void putAt(ISlice aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(ISlice aIndices, IIntVector aVector)
@VisibleForTesting void putAt(List<Integer> aIndices, int aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(List<Integer> aIndices, IIntVector aVector)
@VisibleForTesting void putAt(SliceType aIndices, int aValue)
@VisibleForTesting void putAt(SliceType aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(SliceType aIndices, IIntVector aVector)
@VisibleForTesting void putAt(IIndexFilter aIndices, int aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(IIndexFilter aIndices, IIntVector aVector)
@VisibleForTesting int getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, int aValue)

// === 辅助（protected，子类可覆写显示格式） ===
protected String toString_(int aValue)
```
