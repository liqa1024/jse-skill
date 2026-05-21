# ColumnMatrix

> `jse.math.matrix.ColumnMatrix`

**核心职能**：`final class extends DoubleArrayMatrix`。列主序（column-major）实数矩阵实现。数据以 `double[]` 连续存储，列元素连续排列。`subMat` 返回零拷贝引用视图。转置返回 `RowMatrix` 引用视图（零拷贝）。

```java
// === 静态工厂 ===
static ColumnMatrix zeros(int aSize)
static ColumnMatrix zeros(int aNumRows, int aNumCols)
static ColumnMatrix ones(int aSize)
static ColumnMatrix ones(int aNumRows, int aNumCols)

static Builder builder(int aNumRows)
static Builder builder(int aNumRows, int aInitSize)

// === 构造器 ===
ColumnMatrix(int aNumRows, int aNumCols, int aShift, double[] aData)
ColumnMatrix(int aNumRows, int aNumCols, double[] aData)
ColumnMatrix(int aNumRows, double[] aData)

// === IMatrix ===
final double get(int aRow, int aCol)
final void set(int aRow, int aCol, double aValue)
final double getAndSet(int aRow, int aCol, double aValue)
final int nrows()
final int ncols()
protected ColumnMatrix newZeros_(int aNumRows, int aNumCols)
ColumnMatrix copy()

// === 内部数据 ===
int internalDataSize()
int internalDataShift()
double @Nullable[] getIfHasSameOrderData(Object aObj)

// === 列视图 ===
List<? extends Vector> cols()
Vector col(int aCol)
Vector asVecCol()

// === 运算器 ===
final IMatrixOperation operation()          // fill / assignCol / forEachCol / refTranspose -> RowMatrix

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
    void addCol(IVectorGetter aColGetter)
    void trimToSize()
    ColumnMatrix build()
}
```
