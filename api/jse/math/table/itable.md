# ITable

> `jse.math.table.ITable`

**核心职能**：带列名的二维表格。兼具 Map 式操作（`get(col)/put(col,v)/containsHead/setHead/asMap`）和矩阵式操作（`get(row,col)/set/rows/cols/nrows/ncols/asMatrix`）。无基接口。

```java
// === Map 式操作（列名→向量） ===
IVector get(String aHead)                           // 按列名获取列向量
void put(String aHead, double aValue)               // 填充整列为标量（不存在则新增列）
void put(String aHead, IVector/IVectorGetter/double[]/Iterable<? extends Number>)
boolean containsHead(String aHead)                  // 是否存在该列名
boolean setHead(String aOldHead, String aNewHead)   // 重命名列
Map<String, ? extends IVector> asMap()              // 转为 Map 视图

// === 矩阵式操作 ===
IMatrix asMatrix()                                  // 转为底层矩阵视图
double get(int aRow, String aHead)                  // 按行号+列名获取元素
void set(int aRow, String aHead, double aValue)     // 按行号+列名设置元素
int nrows() / ncols()                               // 行列数
List<? extends IVector> rows() / cols()             // 行列视图
IVector row(int) / col(String)                      // 单行/单列

// === 列头管理 ===
String getHead(int aCol)                            // 按列索引获取列名
int getColumn(String aHead)                         // 按列名获取列索引（不存在返回 -1）
List<String> heads()                                // 列名列表（只读视图）

// === 导出 ===
Map<String, NDArray<double[]>> numpy()              // 每列转为 NDArray
double[][] data()                                   // 转为 double[][]

// === 切片 ===
ITableSlicer slicer() / refSlicer()                 // 值拷贝/引用切片器
ITable copy()

// :note: Groovy 脚本优先使用 t["col"] / t["col"] = x 运算符访问
// === Groovy [] 运算符重载 ===
IVector getAt(String aHead)
void putAt(String, double/IVector/double[]/Iterable)
```
