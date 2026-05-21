# AbstractLogicalMatrix

> `jse.math.matrix.AbstractLogicalMatrix`

**核心职能**：`abstract class implements ILogicalMatrix`。boolean 矩阵骨架实现，提供迭代器、行列视图、批量填充、类型转换等通用方法。算术运算通过 `operation()` 委派给 `AbstractLogicalMatrixOperation`。子类需实现 `get`/`set`/`getAndSet`/`nrows`/`ncols`/`newZeros_`。

```java
// === 打印 ===
String toString()
protected String toString_(boolean aValue)

// === 迭代器 ===

// --- 只读迭代器 ---
IBooleanIterator iteratorCol()                          // 列主序遍历全部
IBooleanIterator iteratorRow()                          // 行主序遍历全部
IBooleanIterator iteratorColAt(int aCol)                // 遍历指定列
IBooleanIterator iteratorRowAt(int aRow)                // 遍历指定行

// --- 可写迭代器 ---
IBooleanSetIterator setIteratorCol()
IBooleanSetIterator setIteratorRow()
IBooleanSetIterator setIteratorColAt(int aCol)
IBooleanSetIterator setIteratorRowAt(int aRow)

// === 行列向量视图 ===
List<? extends ILogicalVector> rows()
ILogicalVector row(int aRow)
List<? extends ILogicalVector> cols()
ILogicalVector col(int aCol)

// === 转换 ===
List<List<Boolean>> asListCols()
List<List<Boolean>> asListRows()
IMatrix asMat()                                          // 0.0/1.0
IIntMatrix asIntMat()                                    // 0/1
ILogicalVector asVecCol()                                // 列主序展开为一维向量
ILogicalVector asVecRow()                                // 行主序展开为一维向量
NDArray<boolean[]> numpy()                               // numpy 互操作
boolean[][] data()                                       // 值拷贝为 boolean[][]
IMatrix.ISize size()

// === 批量填充 ===
final void fill(boolean aValue)
final void fill(ILogicalMatrix aMatrix)
final void fill(ILogicalMatrixGetter aMatrixGetter)
void fill(boolean[][] aData)
void fillWithRows(Iterable<?> aRows)
void fillWithCols(Iterable<?> aCols)

// === 列/行赋值与遍历 ===
final void assignCol(BooleanSupplier aSup)
final void assignRow(BooleanSupplier aSup)
final void forEachCol(IBooleanConsumer aCon)
final void forEachRow(IBooleanConsumer aCon)

// === 单元素更新 ===
void update(int aRow, int aCol, IBooleanUnaryOperator aOpt)
boolean getAndUpdate(int aRow, int aCol, IBooleanUnaryOperator aOpt)

// === 拷贝 / 运算器 ===
ILogicalMatrix copy()
ILogicalMatrixOperation operation()

// === 子类需覆写 ===
abstract boolean get(int aRow, int aCol)
abstract void set(int aRow, int aCol, boolean aValue)
abstract boolean getAndSet(int aRow, int aCol, boolean aValue)  // 返回修改前的值
abstract int nrows()
abstract int ncols()
protected abstract ILogicalMatrix newZeros_(int aNumRows, int aNumCols)
protected ILogicalVector newZerosVec_(int aSize)
```
