# `jse.math.table`

> 带列名的二维表格数据结构（DataFrame-like）。底层委托 `ColumnMatrix`，通过 String 列名进行 Map 式访问和切片。6 个文件。

## 架构总览 (Architecture)

```
ITable (Map式+Matrix式双接口)
  → AbstractTable (骨架, 委托 asMatrix())
    → Table (具体实现, DoubleList+ColumnMatrix)

Tables (final, 独立静态工厂)
```
