# DoubleArrayMatrixOperation

> `jse.math.matrix.DoubleArrayMatrixOperation`

**核心职能**：`abstract class extends AbstractMatrixOperation`。基于 `double[]` 内部存储的矩阵运算优化实现。对每个操作采用双路径策略：当 RHS 和 dest 具有相同内存布局时，走 `ARRAY.*` 直接操作裸数组；否则回退到 `DATA.*` 迭代器路径。

```java
// === 原位运算 — IMatrix RHS（dual-path: ARRAY / DATA）===
void plus2this(IMatrix aRHS)
void minus2this(IMatrix aRHS)
void lminus2this(IMatrix aRHS)
void multiply2this(IMatrix aRHS)
void div2this(IMatrix aRHS)
void ldiv2this(IMatrix aRHS)
void mod2this(IMatrix aRHS)
void lmod2this(IMatrix aRHS)
void operate2this(IMatrix aRHS, DoubleBinaryOperator aOpt)

// === 原位运算 — double RHS（ARRAY 直接路径）===
void plus2this(double aRHS)
void minus2this(double aRHS)
void lminus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)
void ldiv2this(double aRHS)
void mod2this(double aRHS)
void lmod2this(double aRHS)
void map2this(DoubleUnaryOperator aOpt)

// === 单目（dual-path: ARRAY / DATA）===
IMatrix abs()
void abs2this()
IMatrix negative()
void negative2this()

// === 二元运算输出到指定目标 — IMatrix RHS + IMatrix dest（dual-path）===
void plus2dest(IMatrix aRHS, IMatrix rDest)
void minus2dest(IMatrix aRHS, IMatrix rDest)
void lminus2dest(IMatrix aRHS, IMatrix rDest)
void multiply2dest(IMatrix aRHS, IMatrix rDest)
void div2dest(IMatrix aRHS, IMatrix rDest)
void ldiv2dest(IMatrix aRHS, IMatrix rDest)
void mod2dest(IMatrix aRHS, IMatrix rDest)
void lmod2dest(IMatrix aRHS, IMatrix rDest)
void operate2dest(IMatrix aRHS, IMatrix rDest, DoubleBinaryOperator aOpt)

// === 标量运算输出到指定目标 — double RHS + IMatrix dest（dual-path）===
void plus2dest(double aRHS, IMatrix rDest)
void minus2dest(double aRHS, IMatrix rDest)
void lminus2dest(double aRHS, IMatrix rDest)
void multiply2dest(double aRHS, IMatrix rDest)
void div2dest(double aRHS, IMatrix rDest)
void ldiv2dest(double aRHS, IMatrix rDest)
void mod2dest(double aRHS, IMatrix rDest)
void lmod2dest(double aRHS, IMatrix rDest)
void map2dest(IMatrix rDest, DoubleUnaryOperator aOpt)

// === 填充（dual-path）===
void fill(double aRHS)
void fill(IMatrix aRHS)

// === 聚合（ARRAY 直接路径）===
double sum()
double mean()
double max()
double min()

// === 子类需实现的抽象方法 ===
protected abstract DoubleArrayMatrix thisMatrix_()
protected abstract DoubleArrayMatrix newMatrix_(int aRowNum, int aColNum)
```
