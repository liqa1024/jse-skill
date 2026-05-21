# Tables

> `jse.math.table.Tables`

**核心职能**：创建表格的统一入口。默认返回 `Table`。支持从 `IMatrix`/`IMatrixGetter`/`Collection` rows/cols/`Closure` 创建。`final class`，私有构造函数，纯静态方法类。

```java
// === 全零表格 ===
static Table zeros(int nRows) / zeros(int nRows, int nCols) / zeros(int nRows, String... heads)

// === 从已有数据拷贝 ===
static Table from(IMatrix aData, String... heads) / from(IMatrix aData)
static Table from(int nRows, String[] heads, IMatrixGetter) / from(int nRows, int nCols, IMatrixGetter)
static Table from(ITable)                                   // 从已有表格复制
static Table from(Collection<?> rows, String... heads) / fromRows/fromCols(...)
// Groovy Closure 版
static Table from(int nRows, String[] heads, Closure<? extends Number>)
```
