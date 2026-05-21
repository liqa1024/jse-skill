# ILogicalVector

> `jse.math.vector.ILogicalVector`

**核心职能**：`extends ISwapper, IHasBooleanIterator, IHasBooleanSetIterator, ILogicalVectorGetter`（`ILogicalVectorGetter` 同时 extends `IIndexFilter`，可兼作过滤条件）。boolean 类型向量接口，提供独特的逻辑运算体系（and/or/xor/not）、flip 翻转操作、all/any/count 统计、`where()` 索引查找。

```java
// === 元素访问 ===
int size()
boolean get(int aIdx)
void set(int aIdx, boolean aValue)
boolean getAndSet(int aIdx, boolean aValue)
boolean isEmpty()
boolean last()
boolean first()

// === 迭代器 ===
IBooleanIterator iterator()
IBooleanSetIterator setIterator()

// === 单元素操作 ===
void flip(int aIdx)
boolean getAndFlip(int aIdx)
void update(int aIdx, IBooleanUnaryOperator aOpt)
boolean getAndUpdate(int aIdx, IBooleanUnaryOperator aOpt)

// === 批量操作 ===
void fill(boolean aValue)
void fill(ILogicalVector aVector)
void fill(ILogicalVectorGetter aVectorGetter)
void fill(boolean[] aData)
void fill(Iterable<Boolean> aList)
void assign(BooleanSupplier aSup)
void forEach(IBooleanConsumer aCon)

// === 逻辑运算（返回新 ILogicalVector） ===
ILogicalVector and(boolean aRHS)
ILogicalVector or(boolean aRHS)
ILogicalVector xor(boolean aRHS)
ILogicalVector and(ILogicalVector aRHS)
ILogicalVector or(ILogicalVector aRHS)
ILogicalVector xor(ILogicalVector aRHS)
ILogicalVector not()
@VisibleForTesting ILogicalVector bitwiseNegate()

// === 原位逻辑运算（2this，void） ===
void and2this(boolean aRHS)
void or2this(boolean aRHS)
void xor2this(boolean aRHS)
void and2this(ILogicalVector aRHS)
void or2this(ILogicalVector aRHS)
void xor2this(ILogicalVector aRHS)
void not2this()

// === 统计 ===
boolean all()
boolean any()
int count()

// === 索引查找 ===
IIntVector where()

// === 转换 / 视图 ===
List<Boolean> asList()
IVector asVec()
IIntVector asIntVec()
NDArray<boolean[]> numpy()
boolean[] data()

// === 切片 ===
ILogicalVector subVec(int aFromIdx, int aToIdx)
ILogicalVector copy()
// :note: 内部使用且半弃用，优先使用 subVec
ILogicalVectorSlicer slicer()
ILogicalVectorSlicer refSlicer()

// === 运算器 ===
ILogicalVectorOperation operation()
// :note: Groovy 脚本优先使用 op() 简写别名
@VisibleForTesting ILogicalVectorOperation op()

// :note: Groovy 脚本优先使用 v[i] / v[i] = x 运算符访问
// === Groovy 运算符重载 `[]` (@VisibleForTesting) ===
@VisibleForTesting boolean call(int aIdx)
@VisibleForTesting boolean getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, boolean aValue)
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
```
