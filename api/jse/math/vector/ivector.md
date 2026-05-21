# IVector

> `jse.math.vector.IVector`

**核心职能**：`extends ISwapper, IHasDoubleIterator, IHasDoubleSetIterator, IVectorGetter`。定义实数向量的全部契约 — 元素访问、批量填充、算术运算（标量/逐元素/2this/2dest/l* 左变体）、统计归约、比较运算、dot/norm、numpy 转换、Groovy 运算符重载。

```java
// === 元素访问 ===
int size()
double get(int)
void set(int, double)
double getAndSet(int, double)
// 单元素原子操作
void increment(int, ...)
void decrement(int, ...)
void add(int, ...)
void update(int, ...)
double getAndIncrement(int, ...)
double getAndDecrement(int, ...)
double getAndAdd(int, ...)
double getAndUpdate(int, ...)

// === 批量操作 ===
// :note: Groovy 中列表直接匹配 Iterable 重载，无需 as double[] 强转
void fill(double/IVector/IVectorGetter/double[]/Iterable<? extends Number>)
void assign(DoubleSupplier)
void forEach(DoubleConsumer)
// Groovy
default void fill(Closure<? extends Number>)
default void assign(Closure<? extends Number>)

// === 标量算术（返回新 IVector） ===
IVector plus(double)
IVector minus(double)
IVector multiply(double)
IVector div(double)
IVector mod(double)
IVector abs()
IVector negative()

// === 向量逐元素算术 ===
IVector plus(IVector)
IVector minus(IVector)
IVector multiply(IVector)
IVector div(IVector)
IVector mod(IVector)

// === 原位运算（2this，void） ===
void plus2this(double)
void minus2this(double)
void multiply2this(double)
void div2this(double)
void mod2this(double)
void plus2this(IVector)
void minus2this(IVector)
void multiply2this(IVector)
void div2this(IVector)
void mod2this(IVector)
void abs2this()
void negative2this()

// === 统计归约 ===
double sum()
double mean()
double prod()
double max()
double min()
void sort()

// === 比较（返回 ILogicalVector） ===
ILogicalVector equal(double)
ILogicalVector greater(double)
ILogicalVector greaterOrEqual(double)
ILogicalVector less(double)
ILogicalVector lessOrEqual(double)
ILogicalVector equal(IVector)
ILogicalVector greater(IVector)
ILogicalVector greaterOrEqual(IVector)
ILogicalVector less(IVector)
ILogicalVector lessOrEqual(IVector)

// === NaN/Inf 检查 ===
ILogicalVector isNaN()
ILogicalVector isInfinite()
ILogicalVector isFinite()

// === 转换 / 视图 ===
List<Double> asList()                         // 引用列表视图
IIntVector asIntVec()                         // 引用 int 视图（asXxx 语义：引用）
NDArray<double[]> numpy()
double[] data()

// === 切片 ===
IVector subVec(int from, int to)        // 零拷贝子向量
IVector copy()
// :note: 内部使用且半弃用，优先使用 subVec
IVectorSlicer slicer()
IVectorSlicer refSlicer()

// === 运算器 ===
IVectorOperation operation()
// :note: Groovy 脚本优先使用 op() 简写别名
@VisibleForTesting IVectorOperation op()

// :note: Groovy 脚本优先使用 v[i] / v[i] = x 运算符访问
// === Groovy 运算符重载 `[]` (@VisibleForTesting) ===
// Groovy 脚本推荐通过 v[i] / v[i] = x 访问元素，底层映射：
// v[i] 读取
double call(int)
double getAt(int)
double call(ISlice/List/SliceType/IIndexFilter)
double getAt(ISlice/List/SliceType/IIndexFilter)
// v[i] = x 写入
void putAt(int/ISlice/List/SliceType/IIndexFilter, double/Iterable/IVector)
```
