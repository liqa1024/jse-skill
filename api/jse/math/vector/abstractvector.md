# AbstractVector

> `jse.math.vector.AbstractVector`

**核心职能**：`implements IVector`。实数向量 (double) 的骨架实现，提供全部接口方法的默认行为 — 迭代器、转换视图、批量填充/赋值/遍历、单元素原子操作 (increment/decrement/add/update)、切片 (subVec/slicer)、Groovy 运算符重载；算术/统计/比较通过 `operation()` 转发至 `IVectorOperation`，均声明 `final`。子类只需实现 5 个抽象方法。

```java
// === 抽象方法（子类须实现） ===
abstract int size()
abstract double get(int aIdx)
abstract void set(int aIdx, double aValue)
abstract double getAndSet(int aIdx, double aValue)
protected abstract IVector newZeros_(int aSize)

// === 迭代器 ===
IDoubleIterator iterator()
IDoubleSetIterator setIterator()

// === 转换 / 视图 ===
List<Double> asList()
IIntVector asIntVec()
NDArray<double[]> numpy()
double[] data()

// === ISwapper ===
void swap(int aIdx1, int aIdx2)

// === 批量填充 / 赋值 / 遍历（通过 operation() 转发） ===
final void fill(double aValue)
final void fill(IVector aVector)
final void fill(IVectorGetter aVectorGetter)
final void fill(Iterable<? extends Number> aList)
void fill(double[] aData)
final void assign(DoubleSupplier aSup)
final void forEach(DoubleConsumer aCon)

// === 单元素原子操作 ===
void increment(int aIdx)
double getAndIncrement(int aIdx)
void decrement(int aIdx)
double getAndDecrement(int aIdx)
void add(int aIdx, double aDelta)
double getAndAdd(int aIdx, double aDelta)
void update(int aIdx, DoubleUnaryOperator aOpt)
double getAndUpdate(int aIdx, DoubleUnaryOperator aOpt)

// === 切片 ===
IVector copy()
IVector subVec(int aFromIdx, int aToIdx)
// :note: 内部使用且半弃用，优先使用 subVec()
IVectorSlicer slicer()
IVectorSlicer refSlicer()


// === 运算器 ===
IVectorOperation operation()

// === NaN/Inf 检查 ===
ILogicalVector isNaN()
ILogicalVector isInfinite()
ILogicalVector isFinite()

// === 标量算术（new IVector，通过 operation()，final） ===
final IVector plus(double aRHS)
final IVector minus(double aRHS)
final IVector multiply(double aRHS)
final IVector div(double aRHS)
final IVector mod(double aRHS)

// === 向量逐元素算术（new IVector，通过 operation()，final） ===
final IVector plus(IVector aRHS)
final IVector minus(IVector aRHS)
final IVector multiply(IVector aRHS)
final IVector div(IVector aRHS)
final IVector mod(IVector aRHS)

// === 原位运算 2this（通过 operation()，final） ===
final void plus2this(double aRHS)
final void minus2this(double aRHS)
final void multiply2this(double aRHS)
final void div2this(double aRHS)
final void mod2this(double aRHS)
final void plus2this(IVector aRHS)
final void minus2this(IVector aRHS)
final void multiply2this(IVector aRHS)
final void div2this(IVector aRHS)
final void mod2this(IVector aRHS)

// === 一元运算 ===
final IVector abs()
final void abs2this()
final IVector negative()
final void negative2this()

// === 统计归约 ===
final double sum()
final double mean()
final double prod()
final double max()
final double min()
final void sort()

// === 比较（返回 ILogicalVector） ===
final ILogicalVector equal(IVector aRHS)
final ILogicalVector greater(IVector aRHS)
final ILogicalVector greaterOrEqual(IVector aRHS)
final ILogicalVector less(IVector aRHS)
final ILogicalVector lessOrEqual(IVector aRHS)
final ILogicalVector equal(double aRHS)
final ILogicalVector greater(double aRHS)
final ILogicalVector greaterOrEqual(double aRHS)
final ILogicalVector less(double aRHS)
final ILogicalVector lessOrEqual(double aRHS)

// :note: Groovy 脚本优先使用 v[i] / v[i] = x 运算符访问
// === Groovy 运算符重载 `[]`（@VisibleForTesting） ===
@VisibleForTesting double call(int aIdx)
@VisibleForTesting IVector call(ISlice aIndices)
@VisibleForTesting IVector call(List<Integer> aIndices)
@VisibleForTesting IVector call(SliceType aIndices)
@VisibleForTesting IVector call(IIndexFilter aIndices)
@VisibleForTesting IVector getAt(ISlice aIndices)
@VisibleForTesting IVector getAt(List<Integer> aIndices)
@VisibleForTesting IVector getAt(SliceType aIndices)
@VisibleForTesting IVector getAt(IIndexFilter aIndices)
@VisibleForTesting void putAt(ISlice aIndices, double aValue)
@VisibleForTesting void putAt(ISlice aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(ISlice aIndices, IVector aVector)
@VisibleForTesting void putAt(List<Integer> aIndices, double aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(List<Integer> aIndices, IVector aVector)
@VisibleForTesting void putAt(SliceType aIndices, double aValue)
@VisibleForTesting void putAt(SliceType aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(SliceType aIndices, IVector aVector)
@VisibleForTesting void putAt(IIndexFilter aIndices, double aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(IIndexFilter aIndices, IVector aVector)
@VisibleForTesting double getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, double aValue)

// === 静态边界检查（子类复用） ===
@ApiStatus.Internal static void rangeCheck(int aIdx, int aSize)
static void biRangeCheck(int aIdx1, int aIdx2, int aSize)
static void subVecRangeCheck(int aFromIdx, int aToIdx, int aSize)

// === 辅助（protected，子类可覆写显示格式） ===
protected String toString_(double aValue)
```
