# NestedDoubleCPointer

> `jse.cptr.NestedDoubleCPointer`

**核心职能**：`extends AnyCPointer`。对应 C 的 `double **`。除继承的指针数组操作外，新增 `fill`/`parse2dest` 支持二维 `RowMatrix`/`double[]`（按行列参数），`getAt(row,col)`/`putAt(row,col,value)` 直接矩阵索引。`asMat(nrows,ncols)`→`RefMatrix` 零拷贝二维视图。

```java
@UnsafeJNI static NestedDoubleCPointer malloc/calloc(long aCount)

// --- 矩阵填充 ---
@UnsafeJNI void fill(RowMatrix aData)                  // RowMatrix→C
@UnsafeJNI void fill(IDataShell<double[]> aData, int aRowNum, int aColNum)
@UnsafeJNI void fill(double[] aData, int aStart, int aRowNum, int aColNum)
@UnsafeJNI void fill(double aValue, long aRowNum, long aColNum)  // 标量广播

// --- 矩阵解析 ---
@UnsafeJNI void parse2dest(RowMatrix rDest)
@UnsafeJNI void parse2dest(IDataShell<double[]> rDest, int aRowNum, int aColNum)
@UnsafeJNI void parse2dest(double[] rDest, int aStart, int aRowNum, int aColNum)

// --- 矩阵索引 ---
@UnsafeJNI double getAt(long aRow, long aCol)          // ptr[aRow][aCol]
@UnsafeJNI void putAt(long aRow, long aCol, double aValue)

// --- 类型收紧 ---
@UnsafeJNI DoubleCPointer get() / getAt(long) / getAt(int)
NestedDoubleCPointer plus/minus/copy()
@UnsafeJNI List<DoubleCPointer> asList(int aSize)

// --- 矩阵视图 ---
@UnsafeJNI IMatrix asMat(int aRowNum, int aColNum)     // → RefMatrix 零拷贝
```
