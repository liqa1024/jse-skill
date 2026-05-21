# Table

> `jse.math.table.Table`

**核心职能**：`extends AbstractTable implements IDataShell<DoubleList>`。基于 `DoubleList` + `ColumnMatrix` 的表格实现，`asMatrix()` 惰性创建 `ColumnMatrix` 视图（零拷贝）。`Table.zeros(nRows, nCols/heads...)` / `Table(nRows, aData, heads...)`。

```java
// 静态工厂
static Table zeros(int nRows) / zeros(int nRows, int nCols) / zeros(int nRows, String... heads)

// 构造器
Table(int nRows, DoubleList aData, String... heads)
Table(int nRows, int nCols, DoubleList aData)

// IDataShell<DoubleList>
void setInternalData(DoubleList); DoubleList internalData(); int internalDataSize()

// 覆写（返回具体类型 Vector/ColumnMatrix）
ColumnMatrix asMatrix()                    // 惰性创建（零拷贝 DoubleList→ColumnMatrix）
Map<String, Vector> asMap()                // 类型收紧
Vector col(String); List<? extends Vector> cols()
Table copy()
```
