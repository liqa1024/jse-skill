# RowMatrix

> `jse.math.matrix.RowMatrix`

**核心职能**：`final class extends DoubleArrayMatrix`。行主序（row-major）实数矩阵实现，`ColumnMatrix` 的对称实现。数据以 `double[]` 连续存储，行元素连续排列。`numpy()` 在 `shift==0` 时零拷贝返回 `NDArray`。转置返回 `ColumnMatrix` 引用视图（零拷贝）。

```java
// === 静态工厂 ===
static RowMatrix zeros(int aSize)
static RowMatrix zeros(int aNumRows, int aNumCols)
static RowMatrix ones(int aSize)
static RowMatrix ones(int aNumRows, int aNumCols)

static Builder builder(int aNumCols)
static Builder builder(int aNumCols, int aInitSize)

// === 构造器 ===
RowMatrix(int aNumRows, int aNumCols, int aShift, double[] aData)
RowMatrix(int aNumRows, int aNumCols, double[] aData)
RowMatrix(int aNumCols, double[] aData)

// === IMatrix ===
final double get(int aRow, int aCol)
final void set(int aRow, int aCol, double aValue)
final double getAndSet(int aRow, int aCol, double aValue)
final int nrows()
final int ncols()
protected RowMatrix newZeros_(int aNumRows, int aNumCols)
RowMatrix copy()

// === 内部数据 ===
int internalDataSize()
int internalDataShift()
double @Nullable[] getIfHasSameOrderData(Object aObj)
final NDArray<double[]> numpy()                 // shift==0 时零拷贝

// === 行视图 ===
List<? extends Vector> rows()
Vector row(int aRow)
Vector asVecRow()

// === 运算器 ===
final IMatrixOperation operation()          // fill / assignRow / forEachRow / refTranspose -> ColumnMatrix

// === 原子更新 ===
final void update(int aRow, int aCol, DoubleUnaryOperator aOpt)
final double getAndUpdate(int aRow, int aCol, DoubleUnaryOperator aOpt)

// === 迭代器 — 列主序 ===
final IDoubleIterator iteratorCol()
final IDoubleSetIterator setIteratorCol()
final IDoubleIterator iteratorColAt(int aCol)
final IDoubleSetIterator setIteratorColAt(int aCol)

// === 迭代器 — 行主序 ===
final IDoubleIterator iteratorRow()
final IDoubleSetIterator setIteratorRow()
final IDoubleIterator iteratorRowAt(int aRow)
final IDoubleSetIterator setIteratorRowAt(int aRow)

// === Builder ===
final static class Builder {
    void addRow(IVectorGetter aRowGetter)
    void trimToSize()
    RowMatrix build()
}
```
