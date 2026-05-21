# IIntMatrixOperation

> `jse.math.matrix.IIntMatrixOperation`

**核心职能**：整数矩阵运算接口。填充（fill/assign/forEach）、转置（transpose/refTranspose）及对角检测（isDiag）。不含算术运算。

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

// === 转置 ===
IIntMatrix transpose()
IIntMatrix refTranspose()
@VisibleForTesting default IIntMatrix reftranspose()

// === 对角检测 ===
boolean isDiag()
@VisibleForTesting default boolean isdiag()
```
