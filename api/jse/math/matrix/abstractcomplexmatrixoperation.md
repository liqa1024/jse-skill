# AbstractComplexMatrixOperation

> `jse.math.matrix.AbstractComplexMatrixOperation`

**核心职能**：复数矩阵运算骨架抽象类，`implements IComplexMatrixOperation`。实现复数矩阵的逐元素算术（4 种 RHS：`IComplexDouble` / `double` / `IComplexMatrix` / `IMatrix`）、填充、赋值/遍历、负号、转置、对角判断等操作。内部使用 `DATA.*` 复数迭代器工具。抽象方法：`thisMatrix_()` / `newMatrix_()` / `newVector_()`。

```java
// === 二元运算 — IComplexMatrix RHS（返回新矩阵）===
IComplexMatrix plus(IComplexMatrix aRHS)
IComplexMatrix minus(IComplexMatrix aRHS)
IComplexMatrix lminus(IComplexMatrix aRHS)
IComplexMatrix multiply(IComplexMatrix aRHS)
IComplexMatrix div(IComplexMatrix aRHS)
IComplexMatrix ldiv(IComplexMatrix aRHS)
IComplexMatrix operate(IComplexMatrix aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 二元运算 — IMatrix RHS（返回新矩阵）===
IComplexMatrix plus(IMatrix aRHS)
IComplexMatrix minus(IMatrix aRHS)
IComplexMatrix lminus(IMatrix aRHS)
IComplexMatrix multiply(IMatrix aRHS)
IComplexMatrix div(IMatrix aRHS)
IComplexMatrix ldiv(IMatrix aRHS)
IComplexMatrix operate(IMatrix aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, Double> aOpt)

// === 标量运算 — IComplexDouble RHS（返回新矩阵）===
IComplexMatrix plus(IComplexDouble aRHS)
IComplexMatrix minus(IComplexDouble aRHS)
IComplexMatrix lminus(IComplexDouble aRHS)
IComplexMatrix multiply(IComplexDouble aRHS)
IComplexMatrix div(IComplexDouble aRHS)
IComplexMatrix ldiv(IComplexDouble aRHS)

// === 标量运算 — double RHS（返回新矩阵）===
IComplexMatrix plus(double aRHS)
IComplexMatrix minus(double aRHS)
IComplexMatrix lminus(double aRHS)
IComplexMatrix multiply(double aRHS)
IComplexMatrix div(double aRHS)
IComplexMatrix ldiv(double aRHS)

// === 单目映射 ===
IComplexMatrix map(IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)

// === 原位运算 — IComplexMatrix RHS ===
void plus2this(IComplexMatrix aRHS)
void minus2this(IComplexMatrix aRHS)
void lminus2this(IComplexMatrix aRHS)
void multiply2this(IComplexMatrix aRHS)
void div2this(IComplexMatrix aRHS)
void ldiv2this(IComplexMatrix aRHS)
void operate2this(IComplexMatrix aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 原位运算 — IMatrix RHS ===
void plus2this(IMatrix aRHS)
void minus2this(IMatrix aRHS)
void lminus2this(IMatrix aRHS)
void multiply2this(IMatrix aRHS)
void div2this(IMatrix aRHS)
void ldiv2this(IMatrix aRHS)
void operate2this(IMatrix aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, Double> aOpt)

// === 原位运算 — IComplexDouble RHS ===
void plus2this(IComplexDouble aRHS)
void minus2this(IComplexDouble aRHS)
void lminus2this(IComplexDouble aRHS)
void multiply2this(IComplexDouble aRHS)
void div2this(IComplexDouble aRHS)
void ldiv2this(IComplexDouble aRHS)

// === 原位运算 — double RHS ===
void plus2this(double aRHS)
void minus2this(double aRHS)
void lminus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)
void ldiv2this(double aRHS)

// === 单目映射原位 ===
void map2this(IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)

// === 负号 ===
IComplexMatrix negative()
void negative2this()

// === 填充 ===
void fill(IComplexDouble aRHS)
void fill(double aRHS)
void fill(IComplexMatrix aRHS)
void fill(IMatrix aRHS)
void fill(IComplexMatrixGetter aRHS)
void fill(IMatrixGetter aRHS)

// --- Groovy 闭包填充 ---
void fill(@ClosureParams(value=FromString.class, options={"int,int"}) Closure<?> aGroovyTask)

// === 赋值/遍历 — Java 函数式接口 ===
void assignCol(Supplier<? extends IComplexDouble> aSup)
void assignCol(DoubleSupplier aSup)
void assignRow(Supplier<? extends IComplexDouble> aSup)
void assignRow(DoubleSupplier aSup)
void forEachCol(Consumer<? super ComplexDouble> aCon)
void forEachCol(IDoubleBinaryConsumer aCon)
void forEachRow(Consumer<? super ComplexDouble> aCon)
void forEachRow(IDoubleBinaryConsumer aCon)

// --- Groovy 闭包赋值/遍历 ---
void assignCol(Closure<?> aGroovyTask)
void assignRow(Closure<?> aGroovyTask)
void forEachCol(@ClosureParams(value=FromString.class, options={"ComplexDouble", "double,double"}) Closure<?> aGroovyTask)
void forEachRow(@ClosureParams(value=FromString.class, options={"ComplexDouble", "double,double"}) Closure<?> aGroovyTask)

// === 转置 ===
IComplexMatrix transpose()
IComplexMatrix refTranspose()

// === 对角判断 ===
boolean isDiag()

// === 子类需实现的抽象方法 ===
protected abstract IComplexMatrix thisMatrix_()
protected abstract IComplexMatrix newMatrix_(int aRowNum, int aColNum)
protected IComplexVector newVector_(int aSize)
```
