# AbstractMatrixOperation

> `jse.math.matrix.AbstractMatrixOperation`

**核心职能**：实数矩阵运算骨架抽象类，`implements IMatrixOperation`。实现全部算术运算（逐元素和矩阵乘法）、填充、聚合、转置等操作。内部使用 `DATA.*` / `ARRAY.*` 工具方法，子类可覆写以提供内存布局感知的优化路径。抽象方法：`thisMatrix_()` / `newMatrix_()` / `newVector_()`。

```java
// === 二元运算 — IMatrix RHS（返回新矩阵）===
final IMatrix plus(IMatrix aRHS)
final IMatrix minus(IMatrix aRHS)
final IMatrix lminus(IMatrix aRHS)
final IMatrix multiply(IMatrix aRHS)
final IMatrix div(IMatrix aRHS)
final IMatrix ldiv(IMatrix aRHS)
final IMatrix mod(IMatrix aRHS)
final IMatrix lmod(IMatrix aRHS)
final IMatrix operate(IMatrix aRHS, DoubleBinaryOperator aOpt)

// === 单目/标量运算（返回新矩阵）===
final IMatrix plus(double aRHS)
final IMatrix minus(double aRHS)
final IMatrix lminus(double aRHS)
final IMatrix multiply(double aRHS)
final IMatrix div(double aRHS)
final IMatrix ldiv(double aRHS)
final IMatrix mod(double aRHS)
final IMatrix lmod(double aRHS)
final IMatrix map(DoubleUnaryOperator aOpt)

// === 原位运算 — IMatrix RHS ===
void plus2this(IMatrix aRHS)
void minus2this(IMatrix aRHS)
void lminus2this(IMatrix aRHS)
void multiply2this(IMatrix aRHS)
void div2this(IMatrix aRHS)
void ldiv2this(IMatrix aRHS)
void mod2this(IMatrix aRHS)
void lmod2this(IMatrix aRHS)
void operate2this(IMatrix aRHS, DoubleBinaryOperator aOpt)

// === 原位运算 — double RHS ===
void plus2this(double aRHS)
void minus2this(double aRHS)
void lminus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)
void ldiv2this(double aRHS)
void mod2this(double aRHS)
void lmod2this(double aRHS)
void map2this(DoubleUnaryOperator aOpt)

// === 单目 ===
IMatrix abs()
void abs2this()
IMatrix negative()
void negative2this()

// === 二元运算输出到指定目标 — IMatrix RHS + IMatrix dest ===
void plus2dest(IMatrix aRHS, IMatrix rDest)
void minus2dest(IMatrix aRHS, IMatrix rDest)
void lminus2dest(IMatrix aRHS, IMatrix rDest)
void multiply2dest(IMatrix aRHS, IMatrix rDest)
void div2dest(IMatrix aRHS, IMatrix rDest)
void ldiv2dest(IMatrix aRHS, IMatrix rDest)
void mod2dest(IMatrix aRHS, IMatrix rDest)
void lmod2dest(IMatrix aRHS, IMatrix rDest)
void operate2dest(IMatrix aRHS, IMatrix rDest, DoubleBinaryOperator aOpt)

// === 标量运算输出到指定目标 — double RHS + IMatrix dest ===
void plus2dest(double aRHS, IMatrix rDest)
void minus2dest(double aRHS, IMatrix rDest)
void lminus2dest(double aRHS, IMatrix rDest)
void multiply2dest(double aRHS, IMatrix rDest)
void div2dest(double aRHS, IMatrix rDest)
void ldiv2dest(double aRHS, IMatrix rDest)
void mod2dest(double aRHS, IMatrix rDest)
void lmod2dest(double aRHS, IMatrix rDest)
void map2dest(IMatrix rDest, DoubleUnaryOperator aOpt)

// === 填充 ===
void fill(double aRHS)
void fill(IMatrix aRHS)
void fill(IMatrixGetter aRHS)

// === 赋值/遍历 ===
void assignCol(DoubleSupplier aSup)
void assignRow(DoubleSupplier aSup)
void forEachCol(DoubleConsumer aCon)
void forEachRow(DoubleConsumer aCon)

// === 聚合 ===
double sum()
double mean()
double max()
double min()

// === 矩阵乘法 ===
IMatrix matmul(IMatrix aRHS)
IMatrix lmatmul(IMatrix aRHS)
void matmul2this(IMatrix aRHS)
void lmatmul2this(IMatrix aRHS)
void matmul2dest(IMatrix aRHS, IMatrix rDest)
void lmatmul2dest(IMatrix aRHS, IMatrix rDest)

// === 列/行聚合 ===
IVector sumOfCols()
IVector sumOfRows()
IVector meanOfCols()
IVector meanOfRows()

// === 转置 ===
IMatrix transpose()
IMatrix refTranspose()

// === 对角判断 ===
boolean isDiag()

// === 维度检查（static）===
static void ebeCheck(int lNumRows, int lNumCols, int rNumRows, int rNumCols)
static void ebeCheck(int lNumRows, int lNumCols, int rNumRows, int rNumCols, int dNumRows, int dNumCols)
static void mapCheck(int lNumRows, int lNumCols, int dNumRows, int dNumCols)
static void matmulCheck(int lNumRows, int lNumCols, int rNumRows, int rNumCols)
static void matmul2thisCheck(int lNumRows, int lNumCols, int rNumRows, int rNumCols)
static void lmatmul2thisCheck(int lNumRows, int lNumCols, int rNumRows, int rNumCols)
static void matmul2destCheck(int lNumRows, int lNumCols, int rNumRows, int rNumCols, int dNumRows, int dNumCols)

// === 子类需实现的抽象方法 ===
protected abstract IMatrix thisMatrix_()
protected abstract IMatrix newMatrix_(int aNumRows, int aNumCols)
protected IVector newVector_(int aSize)
```
