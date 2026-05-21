# AbstractComplexVector

> `jse.math.vector.AbstractComplexVector`

**核心职能**：复数向量的抽象骨架，实现 `IComplexVector`。提供迭代器、类型转换、实部/虚部分量访问（`real()`/`imag()`）、批量填充（scalar/vector/getter/Closure 等多重重载）、元素级修改、算术运算（plus/minus/multiply/div，支持 `IComplexDouble`/`double`/`IComplexVector`/`IVector` 四种 RHS 类型）、统计（sum/mean）、切片、Groovy 运算符等通用实现。继承需实现 `getReal`/`getImag`/`set`/`setReal`/`setImag`/`getAndSet`/`getAndSetReal`/`getAndSetImag`/`size`/`newZeros_`。

```java
// === Iterator ===
IComplexDoubleIterator iterator()
IComplexDoubleSetIterator setIterator()

// === 类型转换 ===
List<ComplexDouble> asList()
double[][] data()

// === 实部/虚部分量 ===
IVector real()
IVector imag()

// === ISwapper ===
void swap(int aIdx1, int aIdx2)

// === 批量修改 ===
final void fill(IComplexDouble aValue)
final void fill(double aValue)
final void fill(IComplexVector aVector)
final void fill(IVector aVector)
final void fill(IComplexVectorGetter aVectorGetter)
final void fill(IVectorGetter aVectorGetter)
void fill(Iterable<?> aList)
void fill(double[][] aData)
void fill(double[] aData)
final void assign(Supplier<? extends IComplexDouble> aSup)
final void assign(DoubleSupplier aSup)
final void forEach(Consumer<? super ComplexDouble> aCon)
final void forEach(IDoubleBinaryConsumer aCon)
// Groovy Closure overloads
void fill(@ClosureParams(value=SimpleType.class, options="int") Closure<?> aGroovyTask)
final void assign(Closure<?> aGroovyTask)
final void forEach(@ClosureParams(value=FromString.class, options={"ComplexDouble", "double,double"}) Closure<?> aGroovyTask)

// === 元素操作 ===
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

// === 复制与切片 ===
IComplexVector copy()
IComplexVector subVec(int aFromIdx, int aToIdx)
// :note: 内部使用且半弃用，优先使用 subVec()
IComplexVectorSlicer slicer()
IComplexVectorSlicer refSlicer()


// === 运算器 ===
IComplexVectorOperation operation()

// === 算术运算（Groovy 运算符） ===
// plus/minus/multiply/div — 支持 IComplexDouble / double / IComplexVector / IVector 四种 RHS
final IComplexVector plus(IComplexDouble aRHS)
final IComplexVector minus(IComplexDouble aRHS)
final IComplexVector multiply(IComplexDouble aRHS)
final IComplexVector div(IComplexDouble aRHS)
final IComplexVector plus(double aRHS)
final IComplexVector minus(double aRHS)
final IComplexVector multiply(double aRHS)
final IComplexVector div(double aRHS)
final IComplexVector plus(IComplexVector aRHS)
final IComplexVector minus(IComplexVector aRHS)
final IComplexVector multiply(IComplexVector aRHS)
final IComplexVector div(IComplexVector aRHS)
final IComplexVector plus(IVector aRHS)
final IComplexVector minus(IVector aRHS)
final IComplexVector multiply(IVector aRHS)
final IComplexVector div(IVector aRHS)

// In-place operators (2this)
final void plus2this(IComplexDouble aRHS)
final void minus2this(IComplexDouble aRHS)
final void multiply2this(IComplexDouble aRHS)
final void div2this(IComplexDouble aRHS)
final void plus2this(double aRHS)
final void minus2this(double aRHS)
final void multiply2this(double aRHS)
final void div2this(double aRHS)
final void plus2this(IComplexVector aRHS)
final void minus2this(IComplexVector aRHS)
final void multiply2this(IComplexVector aRHS)
final void div2this(IComplexVector aRHS)
final void plus2this(IVector aRHS)
final void minus2this(IVector aRHS)
final void multiply2this(IVector aRHS)
final void div2this(IVector aRHS)

// Unary
final IComplexVector negative()
final void negative2this()

// === 统计 ===
final ComplexDouble sum()
final ComplexDouble mean()

// === Groovy Operators ===
@VisibleForTesting ComplexDouble call(int aIdx)
@VisibleForTesting IComplexVector call(ISlice aIndices)
@VisibleForTesting IComplexVector call(List<Integer> aIndices)
@VisibleForTesting IComplexVector call(SliceType aIndices)
@VisibleForTesting IComplexVector call(IIndexFilter aIndices)
@VisibleForTesting IComplexVector getAt(ISlice aIndices)
@VisibleForTesting IComplexVector getAt(List<Integer> aIndices)
@VisibleForTesting IComplexVector getAt(SliceType aIndices)
@VisibleForTesting IComplexVector getAt(IIndexFilter aIndices)

// putAt(ISlice|List<Integer>|SliceType|IIndexFilter, ...) 支持 6 种值类型
@VisibleForTesting void putAt(ISlice aIndices, IComplexDouble aValue)
@VisibleForTesting void putAt(ISlice aIndices, ComplexDouble aValue)
@VisibleForTesting void putAt(ISlice aIndices, double aValue)
@VisibleForTesting void putAt(ISlice aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(ISlice aIndices, IComplexVector aVector)
@VisibleForTesting void putAt(ISlice aIndices, IVector aVector)
@VisibleForTesting void putAt(List<Integer> aIndices, IComplexDouble aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, ComplexDouble aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, double aValue)
@VisibleForTesting void putAt(List<Integer> aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(List<Integer> aIndices, IComplexVector aVector)
@VisibleForTesting void putAt(List<Integer> aIndices, IVector aVector)
@VisibleForTesting void putAt(SliceType aIndices, IComplexDouble aValue)
@VisibleForTesting void putAt(SliceType aIndices, ComplexDouble aValue)
@VisibleForTesting void putAt(SliceType aIndices, double aValue)
@VisibleForTesting void putAt(SliceType aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(SliceType aIndices, IComplexVector aVector)
@VisibleForTesting void putAt(SliceType aIndices, IVector aVector)
@VisibleForTesting void putAt(IIndexFilter aIndices, IComplexDouble aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, ComplexDouble aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, double aValue)
@VisibleForTesting void putAt(IIndexFilter aIndices, Iterable<? extends Number> aList)
@VisibleForTesting void putAt(IIndexFilter aIndices, IComplexVector aVector)
@VisibleForTesting void putAt(IIndexFilter aIndices, IVector aVector)

// Negative-index single-element access
@VisibleForTesting ComplexDouble getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, IComplexDouble aValue)
@VisibleForTesting void putAt(int aIdx, ComplexDouble aValue)
@VisibleForTesting void putAt(int aIdx, double aValue)

// === 子类需实现 ===
ComplexDouble get(int aIdx)
abstract double getReal(int aIdx)
abstract double getImag(int aIdx)
void set(int aIdx, IComplexDouble aValue)
void set(int aIdx, ComplexDouble aValue)
void set(int aIdx, double aValue)
abstract void set(int aIdx, double aReal, double aImag)
abstract void setReal(int aIdx, double aReal)
abstract void setImag(int aIdx, double aImag)
ComplexDouble getAndSet(int aIdx, IComplexDouble aValue)
ComplexDouble getAndSet(int aIdx, ComplexDouble aValue)
ComplexDouble getAndSet(int aIdx, double aValue)
abstract ComplexDouble getAndSet(int aIdx, double aReal, double aImag)
abstract double getAndSetReal(int aIdx, double aReal)
abstract double getAndSetImag(int aIdx, double aImag)
abstract int size()
protected abstract IComplexVector newZeros_(int aSize)
protected String toString_(double aReal, double aImag)
```
