# AbstractMatrix

> `jse.math.matrix.AbstractMatrix`

**核心职能**：实数矩阵骨架抽象类，`implements IMatrix`。实现大部分 IMatrix 方法（迭代器、行列视图、填充、转换、切片、Groovy 运算符），算术运算通过 `operation()` 委托给 `AbstractMatrixOperation`。子类需实现 `get`/`set`/`getAndSet`/`nrows`/`ncols`/`newZeros_`。

```java
// === 打印 ===
String toString()

// === 迭代器 — 列主序（全量/单列）===
IDoubleIterator iteratorCol()
IDoubleSetIterator setIteratorCol()
IDoubleIterator iteratorColAt(int aCol)
IDoubleSetIterator setIteratorColAt(int aCol)

// === 迭代器 — 行主序（全量/单行）===
IDoubleIterator iteratorRow()
IDoubleSetIterator setIteratorRow()
IDoubleIterator iteratorRowAt(int aRow)
IDoubleSetIterator setIteratorRowAt(int aRow)

// === 转换 ===
List<List<Double>> asListCols()
List<List<Double>> asListRows()
IVector asVecCol()                                 // 列主序展开为一维向量
IVector asVecRow()                                 // 行主序展开为一维向量
NDArray<double[]> numpy()                          // numpy 互操作
double[][] data()                                  // 值拷贝为 double[][]

// === 批量填充 ===
final void fill(double aValue)
final void fill(IMatrix aMatrix)
final void fill(IMatrixGetter aMatrixGetter)
void fill(double[][] aData)
void fillWithRows(Iterable<?> aRows)
void fillWithCols(Iterable<?> aCols)

final void assignCol(DoubleSupplier aSup)
final void assignRow(DoubleSupplier aSup)
final void forEachCol(DoubleConsumer aCon)
final void forEachRow(DoubleConsumer aCon)

// === 维度检查（static）===
static void rangeCheckRow(int aRow, int aNumRows)
static void rangeCheckCol(int aCol, int aNumCols)

// === 行列视图 ===
List<? extends IVector> rows()
IVector row(int aRow)
List<? extends IVector> cols()
IVector col(int aCol)
IMatrix.ISize size()

// 内部 static 类
static abstract class AbstractSize implements ISize {
    String toString()
}

// === 原子更新 ===
void update(int aRow, int aCol, DoubleUnaryOperator aOpt)
double getAndUpdate(int aRow, int aCol, DoubleUnaryOperator aOpt)

// === 拷贝 ===
IMatrix copy()

// === 切片 ===
// :note: 内部使用且半弃用，优先使用 row/col(int)
IMatrixSlicer slicer()
IMatrixSlicer refSlicer()

// === 运算器 ===
IMatrixOperation operation()

// === 标量算术（委托给 operation()） ===
final IMatrix plus(double aRHS)
final IMatrix minus(double aRHS)
final IMatrix multiply(double aRHS)
final IMatrix div(double aRHS)
final IMatrix mod(double aRHS)

// === 矩阵逐元素算术（委托给 operation()） ===
final IMatrix plus(IMatrix aRHS)
final IMatrix minus(IMatrix aRHS)
final IMatrix multiply(IMatrix aRHS)
final IMatrix div(IMatrix aRHS)
final IMatrix mod(IMatrix aRHS)

// === 原位运算 — 标量（委托给 operation()） ===
final void plus2this(double aRHS)
final void minus2this(double aRHS)
final void multiply2this(double aRHS)
final void div2this(double aRHS)
final void mod2this(double aRHS)

// === 原位运算 — 矩阵（委托给 operation()） ===
final void plus2this(IMatrix aRHS)
final void minus2this(IMatrix aRHS)
final void multiply2this(IMatrix aRHS)
final void div2this(IMatrix aRHS)
final void mod2this(IMatrix aRHS)

// === 单目 ===
final IMatrix abs()
final void abs2this()
final IMatrix negative()
final void negative2this()

// === 子类需实现的抽象方法 ===
abstract double get(int aRow, int aCol)
abstract void set(int aRow, int aCol, double aValue)
abstract double getAndSet(int aRow, int aCol, double aValue)  // 返回修改前的值
abstract int nrows()
abstract int ncols()
protected abstract IMatrix newZeros_(int aNumRows, int aNumCols)
protected IVector newZerosVec_(int aSize)
protected String toString_(double aValue)
```
