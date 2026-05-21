# AbstractLogicalMatrixOperation

> `jse.math.matrix.AbstractLogicalMatrixOperation`

**核心职能**：`abstract class implements ILogicalMatrixOperation`。boolean 矩阵运算骨架实现，基于迭代器提供 fill/assign/forEach/transpose/refTranspose/isDiag 的通用实现。子类可覆写 `fill` 等方法进行 ARRAY/DATA 双路径优化。

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
boolean isDiag()

// === 子类需覆写 ===
protected abstract ILogicalMatrix thisMatrix_()
protected abstract ILogicalMatrix newMatrix_(int aRowNum, int aColNum)
protected ILogicalVector newVector_(int aSize)
```
