# RowLogicalMatrix

> `jse.math.matrix.RowLogicalMatrix`

**核心职能**：`final class extends BooleanArrayMatrix`。行主序逻辑矩阵实现，`ColumnLogicalMatrix` 的对称实现。数据以 `boolean[]` 连续存储，行元素连续排列。`numpy()` 在 `shift==0` 时零拷贝返回 `NDArray`。转置返回 `ColumnLogicalMatrix` 引用视图（零拷贝）。

```java
// === 静态工厂 ===
static RowLogicalMatrix zeros(int aSize)
static RowLogicalMatrix zeros(int aNumRows, int aNumCols)
static RowLogicalMatrix ones(int aSize)
static RowLogicalMatrix ones(int aNumRows, int aNumCols)

static Builder builder(int aNumCols)
static Builder builder(int aNumCols, int aInitSize)

// === 构造器 ===
RowLogicalMatrix(int aNumRows, int aNumCols, int aShift, boolean[] aData)
RowLogicalMatrix(int aNumRows, int aNumCols, boolean[] aData)
RowLogicalMatrix(int aNumCols, boolean[] aData)

// === ILogicalMatrix ===
final boolean get(int aRow, int aCol)
final void set(int aRow, int aCol, boolean aValue)
final boolean getAndSet(int aRow, int aCol, boolean aValue)
final int nrows()
final int ncols()
protected RowLogicalMatrix newZeros_(int aNumRows, int aNumCols)
RowLogicalMatrix copy()

// === 内部数据 ===
int internalDataSize()
int internalDataShift()
boolean @Nullable[] getIfHasSameOrderData(Object aObj)
final NDArray<boolean[]> numpy()                    // shift==0 时零拷贝

// === 行视图 ===
List<? extends LogicalVector> rows()
LogicalVector row(int aRow)
LogicalVector asVecRow()

// === 运算器 ===
final ILogicalMatrixOperation operation()       // fill / assignRow / forEachRow / refTranspose -> ColumnLogicalMatrix

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
    void addRow(ILogicalVector aRow)
    void addRow(ILogicalVectorGetter aRowGetter)
    void trimToSize()
    RowLogicalMatrix build()
}
```
