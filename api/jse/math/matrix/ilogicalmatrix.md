# ILogicalMatrix

> `jse.math.matrix.ILogicalMatrix`

**核心职能**：`extends ILogicalMatrixGetter`（`boolean get(int,int)`）。与 `IIntMatrix` 镜像但元素类型为 `boolean`。独有 `asIntMat()`→`IIntMatrix`（0/1）和 `asMat()`→`IMatrix`（0.0/1.0）。

```java
// === 维度/元素访问 ===
int nrows()
int ncols()
IMatrix.ISize size()
boolean get(int aRow, int aCol)
void set(int aRow, int aCol, boolean aValue)
boolean getAndSet(int aRow, int aCol, boolean aValue)

// === 单元素更新 ===
void update(int aRow, int aCol, IBooleanUnaryOperator aOpt)
boolean getAndUpdate(int aRow, int aCol, IBooleanUnaryOperator aOpt)

// === 迭代器（8 个：列/行主序 × 只读/可写 × 全量/单列/单行） ===
IBooleanIterator iteratorCol()
IBooleanIterator iteratorRow()
IBooleanIterator iteratorColAt(int aCol)
IBooleanIterator iteratorRowAt(int aRow)
IBooleanSetIterator setIteratorCol()
IBooleanSetIterator setIteratorRow()
IBooleanSetIterator setIteratorColAt(int aCol)
IBooleanSetIterator setIteratorRowAt(int aRow)
default Iterable<Boolean> iterableCol()
default Iterable<Boolean> iterableRow()

// === 批量填充/赋值/遍历 ===
void fill(boolean aValue)
void fill(ILogicalMatrix aMatrix)
void fill(ILogicalMatrixGetter aMatrixGetter)
void fill(boolean[][] aData)
default void fill(Iterable<?> aRows)
void fillWithRows(Iterable<?> aRows)
void fillWithCols(Iterable<?> aCols)
void assignCol(BooleanSupplier aSup)
void assignRow(BooleanSupplier aSup)
void forEachCol(IBooleanConsumer aCon)
void forEachRow(IBooleanConsumer aCon)

// === 行列视图 ===
List<? extends ILogicalVector> rows()
ILogicalVector row(int aRow)
List<? extends ILogicalVector> cols()
ILogicalVector col(int aCol)

// === 转换/导出 ===
List<List<Boolean>> asListCols()
List<List<Boolean>> asListRows()
IMatrix asMat()
IIntMatrix asIntMat()
ILogicalVector asVecCol()
ILogicalVector asVecRow()
NDArray<boolean[]> numpy()
boolean[][] data()

// === 拷贝/运算器代理 ===
ILogicalMatrix copy()
ILogicalMatrixOperation operation()
// :note: Groovy 脚本优先使用 op() 简写别名
@VisibleForTesting default ILogicalMatrixOperation op()
```


