# ILogicalMatrixOperation

> `jse.math.matrix.ILogicalMatrixOperation`

**核心职能**：逻辑矩阵运算接口。提供 fill/assign/forEach 批量操作和 transpose/refTranspose/isDiag 矩阵运算。注意：无 and/or/xor/not 逻辑运算符（这些在 `ILogicalVector` 中）。

```java
// === 填充 ===
void fill(boolean aRHS)
void fill(ILogicalMatrix aRHS)
void fill(ILogicalMatrixGetter aRHS)

// === 列/行赋值 ===
void assignCol(BooleanSupplier aSup)
void assignRow(BooleanSupplier aSup)

// === 列/行遍历 ===
void forEachCol(IBooleanConsumer aCon)
void forEachRow(IBooleanConsumer aCon)

// === 转置 / 对角 ===
ILogicalMatrix transpose()
ILogicalMatrix refTranspose()
@VisibleForTesting ILogicalMatrix reftranspose()
boolean isDiag()
@VisibleForTesting boolean isdiag()
```
