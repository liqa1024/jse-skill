# IComplexVector

> `jse.math.vector.IComplexVector`

**核心职能**：`extends ISwapper, IHasComplexDoubleIterator, IHasComplexDoubleSetIterator, IComplexVectorGetter`。复数向量接口，实部/虚部分离存储（`double[2][]`）。提供 `real()`/`imag()` 视图访问、4 种 RHS 类型的算术运算（IComplexVector/IVector/IComplexDouble/double）、add/addImag/update/updateReal/updateImag 单元素操作、sum/mean 统计归约、FMA（mplus2this）。

```java
// === 元素访问 ===
int size()
ComplexDouble get(int aIdx)
double getReal(int aIdx)
double getImag(int aIdx)
void set(int aIdx, IComplexDouble aValue)
void set(int aIdx, ComplexDouble aValue)
void set(int aIdx, double aValue)
void set(int aIdx, double aReal, double aImag)
void setReal(int aIdx, double aReal)
void setImag(int aIdx, double aImag)
ComplexDouble getAndSet(int aIdx, IComplexDouble aValue)
ComplexDouble getAndSet(int aIdx, ComplexDouble aValue)
ComplexDouble getAndSet(int aIdx, double aValue)
ComplexDouble getAndSet(int aIdx, double aReal, double aImag)
double getAndSetReal(int aIdx, double aReal)
double getAndSetImag(int aIdx, double aImag)
boolean isEmpty()
ComplexDouble last()
ComplexDouble first()

// === 迭代器 ===
IComplexDoubleIterator iterator()
IComplexDoubleSetIterator setIterator()

// === 单元素操作 ===
void add(int aIdx, IComplexDouble aDelta)
void add(int aIdx, ComplexDouble aDelta)
void add(int aIdx, double aDelta)
void addImag(int aIdx, double aImag)
void update(int aIdx, IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
void updateReal(int aIdx, DoubleUnaryOperator aRealOpt)
void updateImag(int aIdx, DoubleUnaryOperator aImagOpt)
ComplexDouble getAndUpdate(int aIdx, IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
double getAndUpdateReal(int aIdx, DoubleUnaryOperator aRealOpt)
double getAndUpdateImag(int aIdx, DoubleUnaryOperator aImagOpt)

// === 实部/虚部视图 ===
IVector real()
IVector imag()

// === 批量操作 ===
void fill(IComplexDouble aValue)
void fill(double aValue)
void fill(IComplexVector aVector)
void fill(IVector aVector)
void fill(IComplexVectorGetter aVectorGetter)
void fill(IVectorGetter aVectorGetter)
void fill(double[][] aData)
void fill(double[] aData)
void fill(Iterable<?> aList)
void assign(Supplier<? extends IComplexDouble> aSup)
void assign(DoubleSupplier aSup)
void forEach(Consumer<? super ComplexDouble> aCon)
void forEach(IDoubleBinaryConsumer aCon)

// === Groovy 批量操作 ===
void fill(Closure<?> aGroovyTask)
void assign(Closure<?> aGroovyTask)
void forEach(Closure<?> aGroovyTask)

// === 标量算术（返回新 IComplexVector） ===
IComplexVector plus(IComplexDouble aRHS)
IComplexVector minus(IComplexDouble aRHS)
IComplexVector multiply(IComplexDouble aRHS)
IComplexVector div(IComplexDouble aRHS)
IComplexVector plus(double aRHS)
IComplexVector minus(double aRHS)
IComplexVector multiply(double aRHS)
IComplexVector div(double aRHS)

// === 向量逐元素算术 ===
IComplexVector plus(IComplexVector aRHS)
IComplexVector minus(IComplexVector aRHS)
IComplexVector multiply(IComplexVector aRHS)
IComplexVector div(IComplexVector aRHS)
IComplexVector plus(IVector aRHS)
IComplexVector minus(IVector aRHS)
IComplexVector multiply(IVector aRHS)
IComplexVector div(IVector aRHS)

// === 原位运算（2this，void） ===
void plus2this(IComplexDouble aRHS)
void minus2this(IComplexDouble aRHS)
void multiply2this(IComplexDouble aRHS)
void div2this(IComplexDouble aRHS)
void plus2this(double aRHS)
void minus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)
void plus2this(IComplexVector aRHS)
void minus2this(IComplexVector aRHS)
void multiply2this(IComplexVector aRHS)
void div2this(IComplexVector aRHS)
void plus2this(IVector aRHS)
void minus2this(IVector aRHS)
void multiply2this(IVector aRHS)
void div2this(IVector aRHS)

// === 一元运算 ===
IComplexVector negative()
void negative2this()

// === 统计归约 ===
ComplexDouble sum()
ComplexDouble mean()

// === 转换 ===
List<ComplexDouble> asList()
double[][] data()

// === 切片 ===
IComplexVector subVec(int aFromIdx, int aToIdx)
IComplexVector copy()
// :note: 内部使用且半弃用，优先使用 subVec
IComplexVectorSlicer slicer()
IComplexVectorSlicer refSlicer()

// === 运算器 ===
IComplexVectorOperation operation()
// :note: Groovy 脚本优先使用 op() 简写别名
@VisibleForTesting IComplexVectorOperation op()

// :note: Groovy 脚本优先使用 v[i] / v[i] = x 运算符访问
// === Groovy 运算符重载 `[]` (@VisibleForTesting) ===
@VisibleForTesting ComplexDouble call(int aIdx)
@VisibleForTesting ComplexDouble getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, IComplexDouble aValue)
@VisibleForTesting void putAt(int aIdx, ComplexDouble aValue)
@VisibleForTesting void putAt(int aIdx, double aValue)
@VisibleForTesting IComplexVector call(ISlice aIndices)
@VisibleForTesting IComplexVector call(List<Integer> aIndices)
@VisibleForTesting IComplexVector call(SliceType aIndices)
@VisibleForTesting IComplexVector call(IIndexFilter aIndices)
@VisibleForTesting IComplexVector getAt(ISlice aIndices)
@VisibleForTesting IComplexVector getAt(List<Integer> aIndices)
@VisibleForTesting IComplexVector getAt(SliceType aIndices)
@VisibleForTesting IComplexVector getAt(IIndexFilter aIndices)
@VisibleForTesting void putAt(ISlice aIndices, IComplexDouble aValue)
@VisibleForTesting void putAt(ISlice aIndices, ComplexDouble aValue)
@VisibleForTesting void putAt(ISlice aIndices, double aValue)
@VisibleForTesting void putAt(ISlice aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(ISlice aIndices, IVector aVector)
@VisibleForTesting void putAt(ISlice aIndices, IComplexVector aVector)
@VisibleForTesting void putAt(List<Integer> aIndices, IComplexDouble aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, ComplexDouble aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, double aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(List<Integer> aIndices, IVector aVector)
@VisibleForTesting void putAt(List<Integer> aIndices, IComplexVector aVector)
@VisibleForTesting void putAt(SliceType aIndices, IComplexDouble aValue)
@VisibleForTesting void putAt(SliceType aIndices, ComplexDouble aValue)
@VisibleForTesting void putAt(SliceType aIndices, double aValue)
@VisibleForTesting void putAt(SliceType aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(SliceType aIndices, IVector aVector)
@VisibleForTesting void putAt(SliceType aIndices, IComplexVector aVector)
@VisibleForTesting void putAt(IIndexFilter aIndices, IComplexDouble aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, ComplexDouble aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, double aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(IIndexFilter aIndices, IVector aVector)
@VisibleForTesting void putAt(IIndexFilter aIndices, IComplexVector aVector)
```
