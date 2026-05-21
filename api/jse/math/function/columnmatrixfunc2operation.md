# ColumnMatrixFunc2Operation

> `jse.math.function.ColumnMatrixFunc2Operation`

> 此类标记为 @ApiStatus.Experimental

**核心职能**：基于 ColumnMatrix 批量运算的二维函数运算器。继承 AbstractFunc2Operation。两函数同网格时使用 ColumnMatrix.operation() 批量运算加速，否则逐点回退。原地修改可感知 IZeroBoundFunc2 进行 XY 双向裁剪优化。

```java
// === 函数间二元运算（同网格→ColumnMatrix批量运算） ===
IFunc2 plus(IFunc2 aRHS)
IFunc2 minus(IFunc2 aRHS)
IFunc2 lminus(IFunc2 aRHS)
IFunc2 multiply(IFunc2 aRHS)
IFunc2 div(IFunc2 aRHS)
IFunc2 ldiv(IFunc2 aRHS)
IFunc2 mod(IFunc2 aRHS)
IFunc2 lmod(IFunc2 aRHS)
IFunc2 operate(IFunc2 aRHS, DoubleBinaryOperator aOpt)

// === 标量运算（同网格→ColumnMatrix批量运算） ===
IFunc2 plus(double aRHS)
IFunc2 minus(double aRHS)
IFunc2 lminus(double aRHS)
IFunc2 multiply(double aRHS)
IFunc2 div(double aRHS)
IFunc2 ldiv(double aRHS)
IFunc2 mod(double aRHS)
IFunc2 lmod(double aRHS)
IFunc2 map(DoubleUnaryOperator aOpt)

// === 原地二元修改 ===
void plus2this(IFunc2 aRHS)
void minus2this(IFunc2 aRHS)
void lminus2this(IFunc2 aRHS)
void multiply2this(IFunc2 aRHS)
void div2this(IFunc2 aRHS)
void ldiv2this(IFunc2 aRHS)
void mod2this(IFunc2 aRHS)
void lmod2this(IFunc2 aRHS)
void operate2this(IFunc2 aRHS, DoubleBinaryOperator aOpt)

// === 覆盖填充（同网格→ColumnMatrix批量填充） ===
void fill(IFunc2 aRHS)

// === 子类扩展点 ===
protected abstract ColumnMatrixFunc2 thisFunc2_()
protected abstract ColumnMatrixFunc2 newFunc2_()
```
