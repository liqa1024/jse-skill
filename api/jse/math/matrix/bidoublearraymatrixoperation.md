# BiDoubleArrayMatrixOperation

> `jse.math.matrix.BiDoubleArrayMatrixOperation`

**核心职能**：`abstract class extends AbstractComplexMatrixOperation`。复数双精度数组运算层，全部方法采用 ARRAY/DATA 双路径优化：如果 RHS 共享相同 `double[][]` 底层布局则走 `ARRAY.*` 数组直接操作路径，否则回退 `DATA.*` 迭代器路径。

```java
// === 矩阵-复数矩阵运算（返回新 IComplexMatrix）———— ARRAY/DATA 双路径 ===
IComplexMatrix plus(IComplexMatrix aRHS)
IComplexMatrix minus(IComplexMatrix aRHS)
IComplexMatrix lminus(IComplexMatrix aRHS)
IComplexMatrix multiply(IComplexMatrix aRHS)
IComplexMatrix div(IComplexMatrix aRHS)
IComplexMatrix ldiv(IComplexMatrix aRHS)
IComplexMatrix operate(IComplexMatrix aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 标量运算（IComplexDouble） ===
IComplexMatrix plus(IComplexDouble aRHS)
IComplexMatrix minus(IComplexDouble aRHS)
IComplexMatrix lminus(IComplexDouble aRHS)
IComplexMatrix multiply(IComplexDouble aRHS)
IComplexMatrix div(IComplexDouble aRHS)
IComplexMatrix ldiv(IComplexDouble aRHS)

// === 标量运算（double） ===
IComplexMatrix plus(double aRHS)
IComplexMatrix minus(double aRHS)
IComplexMatrix lminus(double aRHS)
IComplexMatrix multiply(double aRHS)
IComplexMatrix div(double aRHS)
IComplexMatrix ldiv(double aRHS)

// === 一元 ===
IComplexMatrix map(IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
IComplexMatrix negative()
void negative2this()

// === 原地运算（2this）— IComplexMatrix RHS ===
void plus2this(IComplexMatrix aRHS)
void minus2this(IComplexMatrix aRHS)
void lminus2this(IComplexMatrix aRHS)
void multiply2this(IComplexMatrix aRHS)
void div2this(IComplexMatrix aRHS)
void ldiv2this(IComplexMatrix aRHS)
void operate2this(IComplexMatrix aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 原地运算（2this）— IComplexDouble RHS ===
void plus2this(IComplexDouble aRHS)
void minus2this(IComplexDouble aRHS)
void lminus2this(IComplexDouble aRHS)
void multiply2this(IComplexDouble aRHS)
void div2this(IComplexDouble aRHS)
void ldiv2this(IComplexDouble aRHS)

// === 原地运算（2this）— double RHS ===
void plus2this(double aRHS)
void minus2this(double aRHS)
void lminus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)
void ldiv2this(double aRHS)

// === 原地 map ===
void map2this(IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)

// === 填充（ARRAY 优先） ===
void fill(IComplexDouble aRHS)                      // ARRAY.mapFill2This
void fill(double aRHS)                              // ARRAY.mapFill2This
void fill(IComplexMatrix aRHS)                      // ARRAY 零拷贝 或 DATA 回退

// === 子类需覆写 ===
protected abstract BiDoubleArrayMatrix thisMatrix_()
protected abstract BiDoubleArrayMatrix newMatrix_(int aRowNum, int aColNum)
```
