# ColumnIntMatrix

> `jse.math.matrix.ColumnIntMatrix`

**核心职能**：`final class extends IntArrayMatrix`。列主序整数矩阵实现。数据以 `int[]` 连续存储，列元素连续排列。转置返回 `RowIntMatrix` 引用视图（零拷贝）。

```java
// === 静态工厂 ===
static ColumnIntMatrix zeros(int aSize)
static ColumnIntMatrix zeros(int aNumRows, int aNumCols)
static ColumnIntMatrix ones(int aSize)
static ColumnIntMatrix ones(int aNumRows, int aNumCols)

static Builder builder(int aNumRows)
static Builder builder(int aNumRows, int aInitSize)

// === 构造器 ===
ColumnIntMatrix(int aNumRows, int aNumCols, int aShift, int[] aData)
ColumnIntMatrix(int aNumRows, int aNumCols, int[] aData)
ColumnIntMatrix(int aNumRows, int[] aData)

// === IIntMatrix ===
final int get(int aRow, int aCol)
final void set(int aRow, int aCol, int aValue)
final int getAndSet(int aRow, int aCol, int aValue)
final int nrows()
final int ncols()
protected ColumnIntMatrix newZeros_(int aNumRows, int aNumCols)
ColumnIntMatrix copy()

// === 内部数据 ===
int internalDataSize()
int internalDataShift()
int @Nullable[] getIfHasSameOrderData(Object aObj)

// === 列视图 ===
List<? extends IntVector> cols()
IntVector col(int aCol)
IntVector asVecCol()

// === 运算器 ===
final IIntMatrixOperation operation()           // fill / assignCol / forEachCol / refTranspose -> RowIntMatrix

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
    void addCol(IIntVector aCol)
    void addCol(IIntVectorGetter aColGetter)
    void trimToSize()
    ColumnIntMatrix build()
}
```
