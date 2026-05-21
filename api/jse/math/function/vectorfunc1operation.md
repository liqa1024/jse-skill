# VectorFunc1Operation

> `jse.math.function.VectorFunc1Operation`

> 此类标记为 @ApiStatus.Experimental

**核心职能**：基于 Vector 批量运算的一维函数运算器。继承 AbstractFunc1Operation。两函数同网格（相同 x0、dx、Nx）时使用 Vector.operation() 批量运算加速，否则逐点回退。原地修改可感知 IZeroBoundFunc1 进行裁剪优化。

```java
// === 函数间二元运算（同网格→Vector批量运算） ===
IFunc1 plus(IFunc1 aRHS)
IFunc1 minus(IFunc1 aRHS)
IFunc1 lminus(IFunc1 aRHS)
IFunc1 multiply(IFunc1 aRHS)
IFunc1 div(IFunc1 aRHS)
IFunc1 ldiv(IFunc1 aRHS)
IFunc1 mod(IFunc1 aRHS)
IFunc1 lmod(IFunc1 aRHS)
IFunc1 operate(IFunc1 aRHS, DoubleBinaryOperator aOpt)

// === 标量运算（同网格→Vector批量运算） ===
IFunc1 plus(double aRHS)
IFunc1 minus(double aRHS)
IFunc1 lminus(double aRHS)
IFunc1 multiply(double aRHS)
IFunc1 div(double aRHS)
IFunc1 ldiv(double aRHS)
IFunc1 mod(double aRHS)
IFunc1 lmod(double aRHS)
IFunc1 map(DoubleUnaryOperator aOpt)

// === 原地二元修改 ===
void plus2this(IFunc1 aRHS)
void minus2this(IFunc1 aRHS)
void lminus2this(IFunc1 aRHS)
void multiply2this(IFunc1 aRHS)
void div2this(IFunc1 aRHS)
void ldiv2this(IFunc1 aRHS)
void mod2this(IFunc1 aRHS)
void lmod2this(IFunc1 aRHS)
void operate2this(IFunc1 aRHS, DoubleBinaryOperator aOpt)

// === 覆盖填充（同网格→Vector批量填充） ===
void fill(IFunc1 aRHS)

// === 微分（有限差分中心差分） ===
protected void gradient2Dest_(IFunc1 rDest, boolean aConsiderBound)
IFunc1 laplacian(boolean aConsiderBound)
protected void laplacian2Dest_(IFunc1 rDest, boolean aConsiderBound)

// === 积分（梯形法） ===
double integral(boolean aConsiderBoundL, boolean aConsiderBoundR)

// === 卷积（惰性引用，梯形法数值积分） ===
IFunc1Subs refConvolve(IFunc2Subs aConv, boolean aConsiderBoundL, boolean aConsiderBoundR)
IFunc1Subs refConvolveFull(IFunc3Subs aConv, boolean aConsiderBoundL, boolean aConsiderBoundR)

// === 子类扩展点 ===
protected abstract VectorFunc1 thisFunc1_()
protected abstract VectorFunc1 newFunc1_()
```
