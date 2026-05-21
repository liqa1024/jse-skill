# IMatrix

> `jse.math.matrix.IMatrix`

**核心职能**：`extends IMatrixGetter`（`double get(int,int)`）。定义实数矩阵的基础契约——元素访问（**不支持 Groovy `[][]` 索引**，必须使用 `get`/`set`）、行列视图。算术运算能力有限，复杂运算通过 `operation()` 获取 `IMatrixOperation`，实践中较少使用，很多模拟对象数据有更自然的 OOP 表达。

```java
// === 维度 ===
int nrows()                                      // 行列数
int ncols()
IMatrix.ISize size()                             // 返回 {row, col}

// === 元素访问 ===
double get(int aRow, int aCol)
void set(int aRow, int aCol, double aValue)
double getAndSet(int aRow, int aCol, double aValue)  // 返回修改前的值
void update(int aRow, int aCol, DoubleUnaryOperator)
double getAndUpdate(int aRow, int aCol, DoubleUnaryOperator)

// === 迭代器（8 个：列/行主序 × 只读/可写 × 全量/单列/单行） ===
IDoubleIterator iteratorCol()                    // 列主序遍历全部
IDoubleIterator iteratorRow()                    // 行主序遍历全部
IDoubleIterator iteratorColAt(int aCol)          // 遍历指定列
IDoubleIterator iteratorRowAt(int aRow)          // 遍历指定行
IDoubleSetIterator setIteratorCol()                 // 可写版本
IDoubleSetIterator setIteratorRow()                 // 可写版本
IDoubleSetIterator setIteratorColAt(int aCol)       // 可写版本
IDoubleSetIterator setIteratorRowAt(int aRow)       // 可写版本
default Iterable<Double> iterableCol()
default Iterable<Double> iterableRow()

// === 行列视图 ===
List<? extends IVector> rows()                   // 行列列表
List<? extends IVector> cols()
IVector row(int)                                 // 单行/单列向量视图
IVector col(int)

// === 批量填充 ===
// :note: Groovy 中列表直接匹配 Iterable 重载，使用 fillWithRows/fillWithCols 代替 fill(double[][])，无需强转
void fill(double aValue)                         // 填充标量
void fill(IMatrix aMatrix)                       // 从另一个矩阵填充
void fill(IMatrixGetter) / fill(double[][] aData)
void fillWithRows(Iterable<?>)                                 // Groovy 首选，直接传入列表
void fillWithCols(Iterable<?>)
void assignCol(DoubleSupplier)
void assignRow(DoubleSupplier)
void forEachCol(DoubleConsumer)
void forEachRow(DoubleConsumer)

// === 标量算术（返回新 IMatrix） ===
IMatrix plus(double)
IMatrix minus(double)
IMatrix multiply(double)
IMatrix div(double)
IMatrix mod(double)
IMatrix abs()
IMatrix negative()

// === 矩阵逐元素算术 ===
IMatrix plus(IMatrix)
IMatrix minus(IMatrix)
IMatrix multiply(IMatrix)
IMatrix div(IMatrix)
IMatrix mod(IMatrix)

// === 原位运算（2this，void） ===
void plus2this(double)
void minus2this(double)
void multiply2this(double)
void div2this(double)
void mod2this(double)
void plus2this(IMatrix)
void minus2this(IMatrix)
void multiply2this(IMatrix)
void div2this(IMatrix)
void mod2this(IMatrix)
void abs2this()
void negative2this()

// === 转换 ===
List<List<Double>> asListCols()
List<List<Double>> asListRows()
IVector asVecCol()                               // 列/行主序展开为一维向量
IVector asVecRow()
NDArray<double[]> numpy()                        // numpy 互操作
double[][] data()                                // 值拷贝为 double[][]

// === 切片 / 运算器 / 拷贝 ===
// :note: 内部使用且半弃用，优先使用 row/col(int)
IMatrixSlicer slicer()
IMatrixSlicer refSlicer()
IMatrixOperation operation()
// :note: Groovy 脚本优先使用 op() 简写别名
@VisibleForTesting IMatrixOperation op()
IMatrix copy()
```
