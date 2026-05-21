# AbstractComplexMatrix

> `jse.math.matrix.AbstractComplexMatrix`

**核心职能**：复数矩阵骨架抽象类，`implements IComplexMatrix`。实部/虚部分离访问（`getReal`/`getImag`/`setReal`/`setImag`），提供迭代器、行列视图、转换、实部/虚部视图（返回 `IMatrix`）、四种 RHS 算术运算及原位操作，均委托给 `AbstractComplexMatrixOperation`。有部分具体方法（`get`/`set(IComplexDouble)`/`set(ComplexDouble)`/`set(double)` 等）委托给抽象方法。

```java
// === 打印 ===
String toString()

// === 迭代器 — 列主序（全量/单列）===
IComplexDoubleIterator iteratorCol()
IComplexDoubleSetIterator setIteratorCol()
IComplexDoubleIterator iteratorColAt(int aCol)
IComplexDoubleSetIterator setIteratorColAt(int aCol)

// === 迭代器 — 行主序（全量/单行）===
IComplexDoubleIterator iteratorRow()
IComplexDoubleSetIterator setIteratorRow()
IComplexDoubleIterator iteratorRowAt(int aRow)
IComplexDoubleSetIterator setIteratorRowAt(int aRow)

// === 转换 ===
List<List<ComplexDouble>> asListCols()
List<List<ComplexDouble>> asListRows()
IComplexVector asVecCol()                            // 列主序展开
IComplexVector asVecRow()                            // 行主序展开

// === 实部/虚部视图（返回 IMatrix 引用） ===
IMatrix real()
IMatrix imag()

// === 数据导出 ===
double[][][] data()                                  // [2][nrows][ncols]: [0]=实部 [1]=虚部

// === 批量填充 — 标量/矩阵/数组源 ===
final void fill(IComplexDouble aValue)
final void fill(double aValue)
final void fill(IComplexMatrix aMatrix)
final void fill(IMatrix aMatrix)
final void fill(IComplexMatrixGetter aMatrixGetter)
final void fill(IMatrixGetter aMatrixGetter)
void fill(double[][][] aData)
void fill(double[][] aData)
void fillWithRows(Iterable<?> aRows)
void fillWithCols(Iterable<?> aCols)

// --- 列/行赋值器（Java 函数式接口） ---
final void assignCol(Supplier<? extends IComplexDouble> aSup)
final void assignCol(DoubleSupplier aSup)
final void assignRow(Supplier<? extends IComplexDouble> aSup)
final void assignRow(DoubleSupplier aSup)
final void forEachCol(Consumer<? super ComplexDouble> aCon)
final void forEachCol(IDoubleBinaryConsumer aCon)
final void forEachRow(Consumer<? super ComplexDouble> aCon)
final void forEachRow(IDoubleBinaryConsumer aCon)

// === Groovy 闭包重载 ===
final void fill(@ClosureParams(value=FromString.class, options={"int,int"}) Closure<?> aGroovyTask)
final void assignCol(Closure<?> aGroovyTask)
final void assignRow(Closure<?> aGroovyTask)
final void forEachCol(@ClosureParams(value=FromString.class, options={"ComplexDouble", "double,double"}) Closure<?> aGroovyTask)
final void forEachRow(@ClosureParams(value=FromString.class, options={"ComplexDouble", "double,double"}) Closure<?> aGroovyTask)

// === 行列视图 ===
List<? extends IComplexVector> rows()
IComplexVector row(int aRow)
List<? extends IComplexVector> cols()
IComplexVector col(int aCol)
IMatrix.ISize size()

// === 原子更新 ===
void update(int aRow, int aCol, IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
void updateReal(int aRow, int aCol, DoubleUnaryOperator aRealOpt)
void updateImag(int aRow, int aCol, DoubleUnaryOperator aImagOpt)
ComplexDouble getAndUpdate(int aRow, int aCol, IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
double getAndUpdateReal(int aRow, int aCol, DoubleUnaryOperator aRealOpt)
double getAndUpdateImag(int aRow, int aCol, DoubleUnaryOperator aImagOpt)

// === 拷贝 ===
IComplexMatrix copy()

// === 运算器 ===
IComplexMatrixOperation operation()

// === 算术运算 — 4 种 RHS（返回新矩阵，委托给 operation()）===
final IComplexMatrix plus(IComplexDouble aRHS)
final IComplexMatrix minus(IComplexDouble aRHS)
final IComplexMatrix multiply(IComplexDouble aRHS)
final IComplexMatrix div(IComplexDouble aRHS)

final IComplexMatrix plus(double aRHS)
final IComplexMatrix minus(double aRHS)
final IComplexMatrix multiply(double aRHS)
final IComplexMatrix div(double aRHS)

final IComplexMatrix plus(IComplexMatrix aRHS)
final IComplexMatrix minus(IComplexMatrix aRHS)
final IComplexMatrix multiply(IComplexMatrix aRHS)
final IComplexMatrix div(IComplexMatrix aRHS)

final IComplexMatrix plus(IMatrix aRHS)
final IComplexMatrix minus(IMatrix aRHS)
final IComplexMatrix multiply(IMatrix aRHS)
final IComplexMatrix div(IMatrix aRHS)

// === 原位运算 — IComplexDouble RHS（委托给 operation()）===
final void plus2this(IComplexDouble aRHS)
final void minus2this(IComplexDouble aRHS)
final void multiply2this(IComplexDouble aRHS)
final void div2this(IComplexDouble aRHS)

// === 原位运算 — double RHS（委托给 operation()）===
final void plus2this(double aRHS)
final void minus2this(double aRHS)
final void multiply2this(double aRHS)
final void div2this(double aRHS)

// === 原位运算 — IComplexMatrix RHS（委托给 operation()）===
final void plus2this(IComplexMatrix aRHS)
final void minus2this(IComplexMatrix aRHS)
final void multiply2this(IComplexMatrix aRHS)
final void div2this(IComplexMatrix aRHS)

// === 原位运算 — IMatrix RHS（委托给 operation()）===
final void plus2this(IMatrix aRHS)
final void minus2this(IMatrix aRHS)
final void multiply2this(IMatrix aRHS)
final void div2this(IMatrix aRHS)

// === 单目 ===
final IComplexMatrix negative()
final void negative2this()

// === 具体实现的元素访问（委托给抽象方法）===
ComplexDouble get(int aRow, int aCol)
void set(int aRow, int aCol, IComplexDouble aValue)
void set(int aRow, int aCol, ComplexDouble aValue)
void set(int aRow, int aCol, double aValue)
ComplexDouble getAndSet(int aRow, int aCol, IComplexDouble aValue)
ComplexDouble getAndSet(int aRow, int aCol, ComplexDouble aValue)
ComplexDouble getAndSet(int aRow, int aCol, double aValue)

// === 子类需实现的抽象方法 ===
abstract double getReal(int aRow, int aCol)
abstract double getImag(int aRow, int aCol)
abstract void set(int aRow, int aCol, double aReal, double aImag)
abstract void setReal(int aRow, int aCol, double aReal)
abstract void setImag(int aRow, int aCol, double aImag)
abstract ComplexDouble getAndSet(int aRow, int aCol, double aReal, double aImag)
abstract double getAndSetReal(int aRow, int aCol, double aReal)
abstract double getAndSetImag(int aRow, int aCol, double aImag)
abstract int nrows()
abstract int ncols()
protected abstract IComplexMatrix newZeros_(int aNumRows, int aNumCols)
protected IComplexVector newZerosVec_(int aSize)
protected String toString_(double aReal, double aImag)
```
