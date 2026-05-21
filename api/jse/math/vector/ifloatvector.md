# IFloatVector

> `jse.math.vector.IFloatVector`

**核心职能**：`extends ISwapper, IHasFloatIterator, IHasFloatSetIterator, IFloatVectorGetter`。float 类型向量接口，结构上与 `IVector` 镜像但**无算术运算**（plus/minus 等）和**统计归约**（sum/mean 等）。需通过这些运算时通过 `asVec()` 获取 double 引用视图转入 `IVector` 主线。

```java
// === 元素访问 ===
int size()
float get(int aIdx)
void set(int aIdx, float aValue)
float getAndSet(int aIdx, float aValue)
boolean isEmpty()
float last()
float first()

// === 迭代器 ===
IFloatIterator iterator()
IFloatSetIterator setIterator()

// === 单元素操作 ===
void update(int aIdx, IFloatUnaryOperator aOpt)
float getAndUpdate(int aIdx, IFloatUnaryOperator aOpt)

// === 批量操作 ===
void fill(float aValue)
void fill(IFloatVector aVector)
void fill(IFloatVectorGetter aVectorGetter)
void fill(float[] aData)
void fill(Iterable<? extends Number> aList)
void assign(IFloatSupplier aSup)
void forEach(IFloatConsumer aCon)

// === Groovy 批量操作 ===
default void fill(Closure<? extends Number> aGroovyTask)
default void assign(Closure<? extends Number> aGroovyTask)

// === 转换 / 视图 ===
List<Float> asList()
IVector asVec()
NDArray<float[]> numpy()
float[] data()

// === 切片 ===
IFloatVector subVec(int aFromIdx, int aToIdx)
IFloatVector copy()
// :note: 内部使用且半弃用，优先使用 subVec
IFloatVectorSlicer slicer()
IFloatVectorSlicer refSlicer()

// === 运算器 ===
IFloatVectorOperation operation()
// :note: Groovy 脚本优先使用 op() 简写别名
@VisibleForTesting IFloatVectorOperation op()

// :note: Groovy 脚本优先使用 v[i] / v[i] = x 运算符访问
// === Groovy 运算符重载 `[]` (@VisibleForTesting) ===
@VisibleForTesting float call(int aIdx)
@VisibleForTesting float getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, float aValue)
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
```
