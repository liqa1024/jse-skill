# IIntMatrix

> `jse.math.matrix.IIntMatrix`

**核心职能**：`extends IIntMatrixGetter`（`int get(int,int)`）。与 `IMatrix` 镜像但元素类型为 `int`，**无算术运算**。通过 `operation()` 获取 `IIntMatrixOperation` 执行矩阵运算，通过 `asMat()` 转换为 `IMatrix`。

```java
// === 维度 ===
int nrows(); int ncols()
IMatrix.ISize size()

// === 元素访问 ===
int get(int aRow, int aCol)
void set(int aRow, int aCol, int aValue)
int getAndSet(int aRow, int aCol, int aValue)           // 返回修改前的值
void update(int aRow, int aCol, IntUnaryOperator)
int getAndUpdate(int aRow, int aCol, IntUnaryOperator)

// === 迭代器（8 个：列/行主序 × 只读/可写 × 全量/单列/单行） ===
IIntIterator iteratorCol()                              // 列主序遍历全部
IIntIterator iteratorRow()                              // 行主序遍历全部
IIntIterator iteratorColAt(int aCol)                    // 遍历指定列
IIntIterator iteratorRowAt(int aRow)                    // 遍历指定行
IIntSetIterator setIteratorCol()                        // 可写版本
IIntSetIterator setIteratorRow()
IIntSetIterator setIteratorColAt(int aCol)
IIntSetIterator setIteratorRowAt(int aRow)
default Iterable<Integer> iterableCol()
default Iterable<Integer> iterableRow()

// === 行列向量视图 ===
List<? extends IIntVector> rows()
IIntVector row(int aRow)
List<? extends IIntVector> cols()
IIntVector col(int aCol)

// === 行/列列表视图 ===
List<List<Integer>> asListCols()
List<List<Integer>> asListRows()
IIntVector asVecCol()                                    // 列主序展开为一维向量
IIntVector asVecRow()                                    // 行主序展开为一维向量
IMatrix asMat()                                          // 转换为 double 矩阵（值拷贝）

// === 批量填充 ===
// :note: Groovy 中列表直接匹配 Iterable 重载，使用 fillWithRows/fillWithCols，无需强转
void fill(int aValue)
void fill(IIntMatrix aMatrix)
void fill(IIntMatrixGetter)
void fill(int[][] aData)
default void fill(Iterable<?> aRows)                     // 委派 fillWithRows
void fillWithRows(Iterable<?>)
void fillWithCols(Iterable<?>)
void assignCol(IntSupplier)
void assignRow(IntSupplier)
void forEachCol(IntConsumer)
void forEachRow(IntConsumer)
// Groovy Closure 重载
default void fill(Closure<? extends Number>)
default void assignCol(Closure<? extends Number>)
default void assignRow(Closure<? extends Number>)

// === 转换 ===
NDArray<int[]> numpy()                                   // numpy 互操作
int[][] data()                                           // 值拷贝为 int[][]

// === 拷贝 / 运算器 ===
IIntMatrix copy()
IIntMatrixOperation operation()
// :note: Groovy 脚本优先使用 op() 简写别名
@VisibleForTesting default IIntMatrixOperation op()
```

| 实现类 | 核心 |
|---|---|
| `AbstractIntMatrix` | 骨架 |
| `IntArrayMatrix` (IDataShell<int[]>) | 数组优化层 |
| `IntArrayMatrixOperation` | ARRAY/DATA 双路径 |
| `ColumnIntMatrix` | 列主序 int[]，refTranspose→RowIntMatrix |
| `RowIntMatrix` | 行主序 int[]，numpy shift=0 零拷贝，refTranspose→ColumnIntMatrix |
| `RefIntMatrix` | 引用视图 |
