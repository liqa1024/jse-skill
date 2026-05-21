# AbstractIntMatrixOperation

> `jse.math.matrix.AbstractIntMatrixOperation`

**核心职能**：`abstract class implements IIntMatrixOperation`。int 矩阵运算骨架实现，基于迭代器提供 fill/assign/forEach/transpose/refTranspose/isDiag 的通用实现。子类可覆写 `fill` 等方法进行 ARRAY/DATA 双路径优化。

```java
// === 填充 ===
void fill(int aRHS)
void fill(IIntMatrix aRHS)
void fill(IIntMatrixGetter aRHS)

// === 列/行赋值 ===
void assignCol(IntSupplier aSup)
void assignRow(IntSupplier aSup)

// === 列/行遍历 ===
void forEachCol(IntConsumer aCon)
void forEachRow(IntConsumer aCon)

// === 转置 / 对角 ===
IIntMatrix transpose()
IIntMatrix refTranspose()
boolean isDiag()

// === 子类需覆写 ===
protected abstract IIntMatrix thisMatrix_()
protected abstract IIntMatrix newMatrix_(int aRowNum, int aColNum)
protected IIntVector newVector_(int aSize)
```
