# IComplexMatrix

> `jse.math.matrix.IComplexMatrix`

**核心职能**：低频复数矩阵体系，`extends IComplexMatrixGetter`（覆写 `get` 返回 `ComplexDouble` 而非 `IComplexDouble`）。实部/虚部分离访问与修改（`getReal`/`getImag`/`setReal`/`setImag`），支持四种 RHS 算术运算（`IComplexDouble`/`double`/`IComplexMatrix`/`IMatrix`）及原位操作；不是普通 `IMatrix` 的 dtype 变体。

```java
// === 维度 ===
int nrows()
int ncols()
IMatrix.ISize size()

// === 元素访问（从 IComplexMatrixGetter 覆写，返回具体类型） ===
ComplexDouble get(int aRow, int aCol)
double getReal(int aRow, int aCol)
double getImag(int aRow, int aCol)

// === 元素修改 ===
void set(int aRow, int aCol, IComplexDouble aValue)
void set(int aRow, int aCol, ComplexDouble aValue)
void set(int aRow, int aCol, double aValue)
void set(int aRow, int aCol, double aReal, double aImag)
void setReal(int aRow, int aCol, double aReal)
void setImag(int aRow, int aCol, double aImag)

// === 原子更新 — getAndSet ===
ComplexDouble getAndSet(int aRow, int aCol, IComplexDouble aValue)
ComplexDouble getAndSet(int aRow, int aCol, ComplexDouble aValue)
ComplexDouble getAndSet(int aRow, int aCol, double aValue)
ComplexDouble getAndSet(int aRow, int aCol, double aReal, double aImag)
double getAndSetReal(int aRow, int aCol, double aReal)
double getAndSetImag(int aRow, int aCol, double aImag)

// === 原子更新 — update ===
void update(int aRow, int aCol, IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
void updateReal(int aRow, int aCol, DoubleUnaryOperator aRealOpt)
void updateImag(int aRow, int aCol, DoubleUnaryOperator aImagOpt)
ComplexDouble getAndUpdate(int aRow, int aCol, IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
double getAndUpdateReal(int aRow, int aCol, DoubleUnaryOperator aRealOpt)
double getAndUpdateImag(int aRow, int aCol, DoubleUnaryOperator aImagOpt)

// === 行列迭代器 ===
IComplexDoubleIterator iteratorCol()
IComplexDoubleIterator iteratorRow()
IComplexDoubleIterator iteratorColAt(int aCol)
IComplexDoubleIterator iteratorRowAt(int aRow)
IComplexDoubleSetIterator setIteratorCol()
IComplexDoubleSetIterator setIteratorRow()
IComplexDoubleSetIterator setIteratorColAt(int aCol)
IComplexDoubleSetIterator setIteratorRowAt(int aRow)

// --- Iterable 包装（default） ---
default Iterable<ComplexDouble> iterableCol()
default Iterable<ComplexDouble> iterableRow()

// === 批量填充 — 值/矩阵/数组源 ===
void fill(IComplexDouble aValue)
void fill(double aValue)
void fill(IComplexMatrix aMatrix)
void fill(IMatrix aMatrix)
void fill(IComplexMatrixGetter aMatrixGetter)
void fill(IMatrixGetter aMatrixGetter)
void fill(double[][][] aData)
void fill(double[][] aData)
default void fill(Iterable<?> aRows)
void fillWithRows(Iterable<?> aRows)
void fillWithCols(Iterable<?> aRows)

// --- 列/行赋值器（Java 函数式接口） ---
void assignCol(Supplier<? extends IComplexDouble> aSup)
void assignCol(DoubleSupplier aSup)
void assignRow(Supplier<? extends IComplexDouble> aSup)
void assignRow(DoubleSupplier aSup)
void forEachCol(Consumer<? super ComplexDouble> aCon)
void forEachCol(IDoubleBinaryConsumer aCon)
void forEachRow(Consumer<? super ComplexDouble> aCon)
void forEachRow(IDoubleBinaryConsumer aCon)

// === Groovy 闭包重载 ===
void fill(@ClosureParams(value=FromString.class, options={"int,int"}) Closure<?> aGroovyTask)
void assignCol(Closure<?> aGroovyTask)
void assignRow(Closure<?> aGroovyTask)
void forEachCol(@ClosureParams(value=FromString.class, options={"ComplexDouble", "double,double"}) Closure<?> aGroovyTask)
void forEachRow(@ClosureParams(value=FromString.class, options={"ComplexDouble", "double,double"}) Closure<?> aGroovyTask)

// === 行列视图 ===
List<? extends IComplexVector> rows()
IComplexVector row(int aRow)
List<? extends IComplexVector> cols()
IComplexVector col(int aCol)
List<List<ComplexDouble>> asListCols()
List<List<ComplexDouble>> asListRows()
IComplexVector asVecCol()
IComplexVector asVecRow()

// === 实部/虚部矩阵视图（IMatrix） ===
IMatrix real()
IMatrix imag()

// === 数据导出 ===
double[][][] data()

// === 算术运算 — IComplexDouble RHS（返回新矩阵） ===
IComplexMatrix plus(IComplexDouble aRHS)
IComplexMatrix minus(IComplexDouble aRHS)
IComplexMatrix multiply(IComplexDouble aRHS)
IComplexMatrix div(IComplexDouble aRHS)

// === 算术运算 — double RHS（返回新矩阵） ===
IComplexMatrix plus(double aRHS)
IComplexMatrix minus(double aRHS)
IComplexMatrix multiply(double aRHS)
IComplexMatrix div(double aRHS)

// === 算术运算 — IComplexMatrix RHS（返回新矩阵） ===
IComplexMatrix plus(IComplexMatrix aRHS)
IComplexMatrix minus(IComplexMatrix aRHS)
IComplexMatrix multiply(IComplexMatrix aRHS)
IComplexMatrix div(IComplexMatrix aRHS)

// === 算术运算 — IMatrix RHS（返回新矩阵） ===
IComplexMatrix plus(IMatrix aRHS)
IComplexMatrix minus(IMatrix aRHS)
IComplexMatrix multiply(IMatrix aRHS)
IComplexMatrix div(IMatrix aRHS)

// === 原位算术（2this）— IComplexDouble RHS ===
void plus2this(IComplexDouble aRHS)
void minus2this(IComplexDouble aRHS)
void multiply2this(IComplexDouble aRHS)
void div2this(IComplexDouble aRHS)

// === 原位算术（2this）— double RHS ===
void plus2this(double aRHS)
void minus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)

// === 原位算术（2this）— IComplexMatrix RHS ===
void plus2this(IComplexMatrix aRHS)
void minus2this(IComplexMatrix aRHS)
void multiply2this(IComplexMatrix aRHS)
void div2this(IComplexMatrix aRHS)

// === 原位算术（2this）— IMatrix RHS ===
void plus2this(IMatrix aRHS)
void minus2this(IMatrix aRHS)
void multiply2this(IMatrix aRHS)
void div2this(IMatrix aRHS)

// === 负号 ===
IComplexMatrix negative()
void negative2this()

// === 运算器/复制 ===
IComplexMatrixOperation operation()
// :note: Groovy 脚本优先使用 op() 简写别名
@VisibleForTesting default IComplexMatrixOperation op()
IComplexMatrix copy()
```
