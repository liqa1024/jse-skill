# ColumnComplexMatrix

> `jse.math.matrix.ColumnComplexMatrix`

**核心职能**：`final class extends BiDoubleArrayMatrix`。列主序复数矩阵实现。数据以 `double[2][]` 存储（`[0]` 实部、`[1]` 虚部），列元素连续排列。`real()`/`imag()` 返回 `ColumnMatrix` 引用视图。转置返回 `RowComplexMatrix` 引用视图（零拷贝）。

```java
// === 静态工厂 ===
static ColumnComplexMatrix zeros(int aSize)
static ColumnComplexMatrix zeros(int aNumRows, int aNumCols)
static ColumnComplexMatrix ones(int aSize)
static ColumnComplexMatrix ones(int aNumRows, int aNumCols)

static Builder builder(int aNumRows)
static Builder builder(int aNumRows, int aInitSize)

// === 构造器 ===
ColumnComplexMatrix(int aNumRows, int aNumCols, int aShift, double[][] aData)
ColumnComplexMatrix(int aNumRows, int aNumCols, double[][] aData)
ColumnComplexMatrix(int aNumRows, double[][] aData)

// === IComplexMatrix ===
final ComplexDouble get(int aRow, int aCol)
final double getReal(int aRow, int aCol)
final double getImag(int aRow, int aCol)
final void set(int aRow, int aCol, IComplexDouble aValue)
final void set(int aRow, int aCol, ComplexDouble aValue)
final void set(int aRow, int aCol, double aValue)
final void set(int aRow, int aCol, double aReal, double aImag)
final void setReal(int aRow, int aCol, double aReal)
final void setImag(int aRow, int aCol, double aImag)
final ComplexDouble getAndSet(int aRow, int aCol, IComplexDouble aValue)
final ComplexDouble getAndSet(int aRow, int aCol, ComplexDouble aValue)
final ComplexDouble getAndSet(int aRow, int aCol, double aValue)
final ComplexDouble getAndSet(int aRow, int aCol, double aReal, double aImag)
final double getAndSetReal(int aRow, int aCol, double aReal)
final double getAndSetImag(int aRow, int aCol, double aImag)
final int nrows()
final int ncols()
protected ColumnComplexMatrix newZeros_(int aNumRows, int aNumCols)
ColumnComplexMatrix copy()

// === 内部数据 ===
int internalDataSize()
int internalDataShift()
double @Nullable[][] getIfHasSameOrderData(Object aObj)

// === 列视图 ===
List<? extends ComplexVector> cols()
ComplexVector col(int aCol)
ComplexVector asVecCol()

// === 实部/虚部 ===
final ColumnMatrix real()
final ColumnMatrix imag()

// === 运算器 ===
final IComplexMatrixOperation operation()   // fill / assignCol / forEachCol / refTranspose -> RowComplexMatrix

// === 原子更新 ===
final void update(int aRow, int aCol, IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
final void updateReal(int aRow, int aCol, DoubleUnaryOperator aRealOpt)
final void updateImag(int aRow, int aCol, DoubleUnaryOperator aImagOpt)
final ComplexDouble getAndUpdate(int aRow, int aCol, IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
final double getAndUpdateReal(int aRow, int aCol, DoubleUnaryOperator aRealOpt)
final double getAndUpdateImag(int aRow, int aCol, DoubleUnaryOperator aImagOpt)

// === 迭代器 — 列主序 ===
final IComplexDoubleIterator iteratorCol()
final IComplexDoubleSetIterator setIteratorCol()
final IComplexDoubleIterator iteratorColAt(int aCol)
final IComplexDoubleSetIterator setIteratorColAt(int aCol)

// === 迭代器 — 行主序 ===
final IComplexDoubleIterator iteratorRow()
final IComplexDoubleSetIterator setIteratorRow()
final IComplexDoubleIterator iteratorRowAt(int aRow)
final IComplexDoubleSetIterator setIteratorRowAt(int aRow)

// === Builder ===
final static class Builder {
    void addCol(IComplexVector aCol)
    void addCol(IVector aCol)
    void addCol(IComplexVectorGetter aColGetter)
    void addCol(IVectorGetter aColGetter)
    void trimToSize()
    ColumnComplexMatrix build()
}
```
