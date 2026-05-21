# AbstractTable

> `jse.math.table.AbstractTable`

**核心职能**：基于 `mHeads`（列名列表）+ `mHead2Idx`（列名→索引映射）实现全部 `ITable` 方法，委托给子类提供的 `asMatrix()`。`slicer()`/`refSlicer()` 返回 `AbstractTableSlicer` 匿名实现。
**抽象方法**：`abstract IMatrix asMatrix()`，`protected IVector newColumn_(String aHead)`（新增列，默认抛异常）
