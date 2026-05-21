# IComplexMatrixOperation

> `jse.math.matrix.IComplexMatrixOperation`

**核心职能**：复数矩阵运算接口。提供 4 类 RHS（IComplexMatrix/IMatrix/IComplexDouble/double）的算术运算（plus/minus/lminus/multiply/div/ldiv/operate）及原地 `*2this` 变体，以及 map/fill/assign/forEach/negative/transpose/isDiag。注意无 matmul/sumOfCols/meanOfCols（这些在 `IMatrixOperation` 中）。

```java
// === 矩阵-复数矩阵运算（返回新 IComplexMatrix） ===
IComplexMatrix plus(IComplexMatrix aRHS)
IComplexMatrix minus(IComplexMatrix aRHS)
IComplexMatrix lminus(IComplexMatrix aRHS)
IComplexMatrix multiply(IComplexMatrix aRHS)
IComplexMatrix div(IComplexMatrix aRHS)
IComplexMatrix ldiv(IComplexMatrix aRHS)
IComplexMatrix operate(IComplexMatrix aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 矩阵-实数矩阵运算 ===
IComplexMatrix plus(IMatrix aRHS)
IComplexMatrix minus(IMatrix aRHS)
IComplexMatrix lminus(IMatrix aRHS)
IComplexMatrix multiply(IMatrix aRHS)
IComplexMatrix div(IMatrix aRHS)
IComplexMatrix ldiv(IMatrix aRHS)
IComplexMatrix operate(IMatrix aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, Double> aOpt)

// === 标量运算 ===
IComplexMatrix plus(IComplexDouble aRHS)
IComplexMatrix minus(IComplexDouble aRHS)
IComplexMatrix lminus(IComplexDouble aRHS)
IComplexMatrix multiply(IComplexDouble aRHS)
IComplexMatrix div(IComplexDouble aRHS)
IComplexMatrix ldiv(IComplexDouble aRHS)
IComplexMatrix plus(double aRHS)
IComplexMatrix minus(double aRHS)
IComplexMatrix lminus(double aRHS)
IComplexMatrix multiply(double aRHS)
IComplexMatrix div(double aRHS)
IComplexMatrix ldiv(double aRHS)
IComplexMatrix map(IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)

// === 原地运算（2this，void）—— 矩阵-复数矩阵 ===
void plus2this(IComplexMatrix aRHS)
void minus2this(IComplexMatrix aRHS)
void lminus2this(IComplexMatrix aRHS)
void multiply2this(IComplexMatrix aRHS)
void div2this(IComplexMatrix aRHS)
void ldiv2this(IComplexMatrix aRHS)
void operate2this(IComplexMatrix aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 原地运算 —— 矩阵-实数矩阵 ===
void plus2this(IMatrix aRHS)
void minus2this(IMatrix aRHS)
void lminus2this(IMatrix aRHS)
void multiply2this(IMatrix aRHS)
void div2this(IMatrix aRHS)
void ldiv2this(IMatrix aRHS)
void operate2this(IMatrix aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, Double> aOpt)

// === 原地运算 —— 标量 ===
void plus2this(IComplexDouble aRHS)
void minus2this(IComplexDouble aRHS)
void lminus2this(IComplexDouble aRHS)
void multiply2this(IComplexDouble aRHS)
void div2this(IComplexDouble aRHS)
void ldiv2this(IComplexDouble aRHS)
void plus2this(double aRHS)
void minus2this(double aRHS)
void lminus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)
void ldiv2this(double aRHS)
void map2this(IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)

// === 一元运算 ===
IComplexMatrix negative()
void negative2this()

// === 填充 ===
void fill(IComplexDouble aRHS)
void fill(double aRHS)
void fill(IComplexMatrix aRHS)
void fill(IMatrix aRHS)
void fill(IComplexMatrixGetter aRHS)
void fill(IMatrixGetter aRHS)

// === 列/行赋值 ===
void assignCol(Supplier<? extends IComplexDouble> aSup)
void assignCol(DoubleSupplier aSup)
void assignRow(Supplier<? extends IComplexDouble> aSup)
void assignRow(DoubleSupplier aSup)

// === 列/行遍历 ===
void forEachCol(Consumer<? super ComplexDouble> aCon)
void forEachCol(IDoubleBinaryConsumer aCon)
void forEachRow(Consumer<? super ComplexDouble> aCon)
void forEachRow(IDoubleBinaryConsumer aCon)

// === Groovy 重载 ===
void fill(Closure<?> aGroovyTask)
void assignCol(Closure<?> aGroovyTask)
void assignRow(Closure<?> aGroovyTask)
void forEachCol(Closure<?> aGroovyTask)
void forEachRow(Closure<?> aGroovyTask)

// === 转置 / 对角 ===
IComplexMatrix transpose()
IComplexMatrix refTranspose()
@VisibleForTesting IComplexMatrix reftranspose()
boolean isDiag()
@VisibleForTesting boolean isdiag()
```
