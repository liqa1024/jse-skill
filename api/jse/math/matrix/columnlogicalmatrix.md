# ColumnLogicalMatrix

> `jse.math.matrix.ColumnLogicalMatrix`

**核心职能**：`final class extends BooleanArrayMatrix`。列主序逻辑矩阵实现。数据以 `boolean[]` 连续存储，列元素连续排列。转置返回 `RowLogicalMatrix` 引用视图（零拷贝）。

```java
// === 静态工厂 ===
static ColumnLogicalMatrix zeros(int aSize)
static ColumnLogicalMatrix zeros(int aNumRows, int aNumCols)
static ColumnLogicalMatrix ones(int aSize)
static ColumnLogicalMatrix ones(int aNumRows, int aNumCols)

static Builder builder(int aNumRows)
static Builder builder(int aNumRows, int aInitSize)

// === 构造器 ===
ColumnLogicalMatrix(int aNumRows, int aNumCols, int aShift, boolean[] aData)
ColumnLogicalMatrix(int aNumRows, int aNumCols, boolean[] aData)
ColumnLogicalMatrix(int aNumRows, boolean[] aData)

// === ILogicalMatrix ===
final boolean get(int aRow, int aCol)
final void set(int aRow, int aCol, boolean aValue)
final boolean getAndSet(int aRow, int aCol, boolean aValue)
final int nrows()
final int ncols()
protected ColumnLogicalMatrix newZeros_(int aNumRows, int aNumCols)
ColumnLogicalMatrix copy()

// === 内部数据 ===
int internalDataSize()
int internalDataShift()
boolean @Nullable[] getIfHasSameOrderData(Object aObj)

// === 列视图 ===
List<? extends LogicalVector> cols()
LogicalVector col(int aCol)
LogicalVector asVecCol()

// === 运算器 ===
final ILogicalMatrixOperation operation()       // fill / assignCol / forEachCol / refTranspose -> RowLogicalMatrix

// === 原子更新 ===
final void update(int aRow, int aCol, IBooleanUnaryOperator aOpt)
final boolean getAndUpdate(int aRow, int aCol, IBooleanUnaryOperator aOpt)

// === 迭代器 — 列主序 ===
final IBooleanIterator iteratorCol()
final IBooleanSetIterator setIteratorCol()
final IBooleanIterator iteratorColAt(int aCol)
final IBooleanSetIterator setIteratorColAt(int aCol)

// === 迭代器 — 行主序 ===
final IBooleanIterator iteratorRow()
final IBooleanSetIterator setIteratorRow()
final IBooleanIterator iteratorRowAt(int aRow)
final IBooleanSetIterator setIteratorRowAt(int aRow)

// === Builder ===
final static class Builder {
    void addCol(ILogicalVector aCol)
    void addCol(ILogicalVectorGetter aColGetter)
    void trimToSize()
    ColumnLogicalMatrix build()
}
```
