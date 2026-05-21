# RowIntMatrix

> `jse.math.matrix.RowIntMatrix`

**核心职能**：`final class extends IntArrayMatrix`。行主序整数矩阵实现，`ColumnIntMatrix` 的对称实现。数据以 `int[]` 连续存储，行元素连续排列。`numpy()` 在 `shift==0` 时零拷贝返回 `NDArray`。转置返回 `ColumnIntMatrix` 引用视图（零拷贝）。

```java
// === 静态工厂 ===
static RowIntMatrix zeros(int aSize)
static RowIntMatrix zeros(int aNumRows, int aNumCols)
static RowIntMatrix ones(int aSize)
static RowIntMatrix ones(int aNumRows, int aNumCols)

static Builder builder(int aNumCols)
static Builder builder(int aNumCols, int aInitSize)

// === 构造器 ===
RowIntMatrix(int aNumRows, int aNumCols, int aShift, int[] aData)
RowIntMatrix(int aNumRows, int aNumCols, int[] aData)
RowIntMatrix(int aNumCols, int[] aData)

// === IIntMatrix ===
final int get(int aRow, int aCol)
final void set(int aRow, int aCol, int aValue)
final int getAndSet(int aRow, int aCol, int aValue)
final int nrows()
final int ncols()
protected RowIntMatrix newZeros_(int aNumRows, int aNumCols)
RowIntMatrix copy()

// === 内部数据 ===
int internalDataSize()
int internalDataShift()
int @Nullable[] getIfHasSameOrderData(Object aObj)
final NDArray<int[]> numpy()                        // shift==0 时零拷贝

// === 行视图 ===
List<? extends IntVector> rows()
IntVector row(int aRow)
IntVector asVecRow()

// === 运算器 ===
final IIntMatrixOperation operation()           // fill / assignRow / forEachRow / refTranspose -> ColumnIntMatrix

// === 原子更新 ===
final void update(int aRow, int aCol, IntUnaryOperator aOpt)
final int getAndUpdate(int aRow, int aCol, IntUnaryOperator aOpt)

// === 迭代器 — 列主序 ===
final IIntIterator iteratorCol()
final IIntSetIterator setIteratorCol()
final IIntIterator iteratorColAt(int aCol)
final IIntSetIterator setIteratorColAt(int aCol)

// === 迭代器 — 行主序 ===
final IIntIterator iteratorRow()
final IIntSetIterator setIteratorRow()
final IIntIterator iteratorRowAt(int aRow)
final IIntSetIterator setIteratorRowAt(int aRow)

// === Builder ===
final static class Builder {
    void addRow(IIntVector aRow)
    void addRow(IIntVectorGetter aRowGetter)
    void trimToSize()
    RowIntMatrix build()
}
```
