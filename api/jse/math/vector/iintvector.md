# IIntVector

> `jse.math.vector.IIntVector`

**核心职能**：`extends ISwapper, ISlice, IHasIntIterator, IHasIntSetIterator, IIntVectorGetter`。int 类型向量接口，与 `IVector` 镜像：含标量/向量算术运算、统计归约、sort/shuffle、increment/decrement/add/update 单元素原子操作。

```java
// === 元素访问 ===
int size()
int get(int aIdx)
void set(int aIdx, int aValue)
int getAndSet(int aIdx, int aValue)
boolean isEmpty()
int last()
int first()

// === 迭代器 ===
IIntIterator iterator()
IIntSetIterator setIterator()

// === 单元素原子操作 ===
void increment(int aIdx)
int getAndIncrement(int aIdx)
void decrement(int aIdx)
int getAndDecrement(int aIdx)
void add(int aIdx, int aDelta)
int getAndAdd(int aIdx, int aDelta)
void update(int aIdx, IntUnaryOperator aOpt)
int getAndUpdate(int aIdx, IntUnaryOperator aOpt)

// === 批量操作 ===
void fill(int aValue)
void fill(IIntVector aVector)
void fill(IIntVectorGetter aVectorGetter)
void fill(int[] aData)
void fill(Iterable<? extends Number> aList)
void assign(IntSupplier aSup)
void forEach(IntConsumer aCon)

// === Groovy 批量操作 ===
default void fill(Closure<? extends Number> aGroovyTask)
default void assign(Closure<? extends Number> aGroovyTask)

// === 标量算术（返回新 IIntVector） ===
IIntVector plus(int aRHS)
IIntVector minus(int aRHS)
IIntVector multiply(int aRHS)
IIntVector div(int aRHS)
IIntVector mod(int aRHS)

// === 向量逐元素算术 ===
IIntVector plus(IIntVector aRHS)
IIntVector minus(IIntVector aRHS)
IIntVector multiply(IIntVector aRHS)
IIntVector div(IIntVector aRHS)
IIntVector mod(IIntVector aRHS)

// === 原位运算（2this，void） ===
void plus2this(int aRHS)
void minus2this(int aRHS)
void multiply2this(int aRHS)
void div2this(int aRHS)
void mod2this(int aRHS)
void plus2this(IIntVector aRHS)
void minus2this(IIntVector aRHS)
void multiply2this(IIntVector aRHS)
void div2this(IIntVector aRHS)
void mod2this(IIntVector aRHS)

// === 一元运算 ===
IIntVector abs()
void abs2this()
IIntVector negative()
void negative2this()

// === 统计归约 ===
int sum()
double mean()
double prod()
int max()
int min()

// === 排序 / 乱序 ===
void sort()
void shuffle()
void shuffle(IRandom aRng)

// === 转换 / 视图 ===
List<Integer> asList()
IVector asVec()
NDArray<int[]> numpy()
int[] data()

// === 切片 ===
IIntVector subVec(int aFromIdx, int aToIdx)
IIntVector copy()
// :note: 内部使用且半弃用，优先使用 subVec
IIntVectorSlicer slicer()
IIntVectorSlicer refSlicer()

// === 运算器 ===
IIntVectorOperation operation()
// :note: Groovy 脚本优先使用 op() 简写别名
@VisibleForTesting IIntVectorOperation op()

// :note: Groovy 脚本优先使用 v[i] / v[i] = x 运算符访问
// === Groovy 运算符重载 `[]` (@VisibleForTesting) ===
@VisibleForTesting int call(int aIdx)
@VisibleForTesting int getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, int aValue)
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
```
