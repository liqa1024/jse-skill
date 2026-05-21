# ILongVector

> `jse.math.vector.ILongVector`

**核心职能**：`extends ISwapper, IHasLongIterator, IHasLongSetIterator, ILongVectorGetter`。long 类型向量接口，结构与 `IIntVector` 镜像但**无算术运算符**（plus/minus 等），仅通过 `operation()` 间接使用运算。含 increment/decrement/add/update 单元素原子操作、统计归约、sort 排序。

```java
// === 元素访问 ===
int size()
long get(int aIdx)
void set(int aIdx, long aValue)
long getAndSet(int aIdx, long aValue)
boolean isEmpty()
long last()
long first()

// === 迭代器 ===
ILongIterator iterator()
ILongSetIterator setIterator()

// === 单元素原子操作 ===
void increment(int aIdx)
long getAndIncrement(int aIdx)
void decrement(int aIdx)
long getAndDecrement(int aIdx)
void add(int aIdx, long aDelta)
long getAndAdd(int aIdx, long aDelta)
void update(int aIdx, LongUnaryOperator aOpt)
long getAndUpdate(int aIdx, LongUnaryOperator aOpt)

// === 批量操作 ===
void fill(long aValue)
void fill(ILongVector aVector)
void fill(ILongVectorGetter aVectorGetter)
void fill(long[] aData)
void fill(Iterable<? extends Number> aList)
void assign(LongSupplier aSup)
void forEach(LongConsumer aCon)

// === Groovy 批量操作 ===
default void fill(Closure<? extends Number> aGroovyTask)
default void assign(Closure<? extends Number> aGroovyTask)

// === 统计归约 ===
long sum()
double mean()
double prod()
long max()
long min()

// === 排序 ===
void sort()

// === 转换 / 视图 ===
List<Long> asList()
IVector asVec()
IIntVector asIntVec()
NDArray<long[]> numpy()
long[] data()

// === 切片 ===
ILongVector subVec(int aFromIdx, int aToIdx)
ILongVector copy()
// :note: 内部使用且半弃用，优先使用 subVec
ILongVectorSlicer slicer()
ILongVectorSlicer refSlicer()

// === 运算器 ===
ILongVectorOperation operation()
// :note: Groovy 脚本优先使用 op() 简写别名
@VisibleForTesting ILongVectorOperation op()

// :note: Groovy 脚本优先使用 v[i] / v[i] = x 运算符访问
// === Groovy 运算符重载 `[]` (@VisibleForTesting) ===
@VisibleForTesting long call(int aIdx)
@VisibleForTesting long getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, long aValue)
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
```
