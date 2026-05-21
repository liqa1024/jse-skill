# AbstractIntMatrix

> `jse.math.matrix.AbstractIntMatrix`

**核心职能**：`abstract class implements IIntMatrix`。int 矩阵骨架实现，提供迭代器、行列视图、批量填充、类型转换等通用方法。算术运算通过 `operation()` 委派给 `AbstractIntMatrixOperation`。子类需实现 `get`/`set`/`getAndSet`/`nrows`/`ncols`/`newZeros_`。

```java
// === 打印 ===
String toString()
protected String toString_(int aValue)

// === 迭代器 ===

// --- 只读迭代器 ---
IIntIterator iteratorCol()                          // 列主序遍历全部
IIntIterator iteratorRow()                          // 行主序遍历全部
IIntIterator iteratorColAt(int aCol)                // 遍历指定列
IIntIterator iteratorRowAt(int aRow)                // 遍历指定行

// --- 可写迭代器 ---
IIntSetIterator setIteratorCol()
IIntSetIterator setIteratorRow()
IIntSetIterator setIteratorColAt(int aCol)
IIntSetIterator setIteratorRowAt(int aRow)

// === 行列向量视图 ===
List<? extends IIntVector> rows()
IIntVector row(int aRow)
List<? extends IIntVector> cols()
IIntVector col(int aCol)

// === 转换 ===
List<List<Integer>> asListCols()
List<List<Integer>> asListRows()
IMatrix asMat()                                      // 转换为 double 矩阵（引用视图）
IIntVector asVecCol()                                // 列主序展开为一维向量
IIntVector asVecRow()                                // 行主序展开为一维向量
NDArray<int[]> numpy()                               // numpy 互操作
int[][] data()                                       // 值拷贝为 int[][]
IMatrix.ISize size()

// === 批量填充 ===
final void fill(int aValue)
final void fill(IIntMatrix aMatrix)
final void fill(IIntMatrixGetter aMatrixGetter)
void fill(int[][] aData)
void fillWithRows(Iterable<?> aRows)
void fillWithCols(Iterable<?> aCols)

// === 列/行赋值与遍历 ===
final void assignCol(IntSupplier aSup)
final void assignRow(IntSupplier aSup)
final void forEachCol(IntConsumer aCon)
final void forEachRow(IntConsumer aCon)

// === 单元素更新 ===
void update(int aRow, int aCol, IntUnaryOperator aOpt)
int getAndUpdate(int aRow, int aCol, IntUnaryOperator aOpt)

// === 拷贝 / 运算器 ===
IIntMatrix copy()
IIntMatrixOperation operation()

// === 子类需覆写 ===
abstract int get(int aRow, int aCol)
abstract void set(int aRow, int aCol, int aValue)
abstract int getAndSet(int aRow, int aCol, int aValue)  // 返回修改前的值
abstract int nrows()
abstract int ncols()
protected abstract IIntMatrix newZeros_(int aNumRows, int aNumCols)
protected IIntVector newZerosVec_(int aSize)
```
