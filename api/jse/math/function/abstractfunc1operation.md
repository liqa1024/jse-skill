# AbstractFunc1Operation

> `jse.math.function.AbstractFunc1Operation`

> 此类标记为 @ApiStatus.Experimental

**核心职能**：一维函数运算器抽象骨架。`abstract class implements IFunc1Operation`。提供二元运算、标量运算、带坐标运算、微分（gradient/laplacian）、积分（梯形法）、卷积（refConvolve/convolveFull）及极值（maxX/minX）的默认实现。

```java
// === 函数间二元运算（返回新 IFunc1） ===
IFunc1 plus/minus/lminus/multiply/div/ldiv/mod/lmod(IFunc1)
IFunc1 operate(IFunc1, DoubleBinaryOperator)

// === 原地二元运算（修改自身） ===
void plus2this/minus2this/lminus2this/multiply2this/div2this/ldiv2this/mod2this/lmod2this(IFunc1)
void operate2this(IFunc1, DoubleBinaryOperator)

// === 标量二元运算（返回新 IFunc1） ===
IFunc1 plus/minus/lminus/multiply/div/ldiv/mod/lmod(double)
IFunc1 map(DoubleUnaryOperator)

// === 标量原地运算 ===
void plus2this/minus2this/lminus2this/multiply2this/div2this/ldiv2this/mod2this/lmod2this(double)
void map2this(DoubleUnaryOperator)

// === fill/assign/forEach ===
void fill(double)
void fill(IVector)
void fill(IFunc1)
void fill(IFunc1Subs)
void assign(DoubleSupplier)
void forEach(DoubleConsumer)

// === 带坐标运算（三元: f+rhs+x / 二元: f+x） ===
IFunc1 operateFull(IFunc1, IDoubleTernaryOperator)
IFunc1 mapFull(DoubleBinaryOperator)
void operateFull2this(IFunc1, IDoubleTernaryOperator)
void mapFull2this(DoubleBinaryOperator)

// === 微分（有限差分） ===
IFunc1 gradient()
IFunc1 gradient(boolean)
protected void gradient2Dest_(IFunc1, boolean)

IFunc1 laplacian()
IFunc1 laplacian(boolean)

// === 积分（梯形法） ===
double integral()
double integral(boolean, boolean)

// === 卷积（IFunc2Subs 二元卷积核） ===
IFunc1 convolve(IFunc2Subs)
IFunc1 convolve(IFunc2Subs, boolean, boolean)
IFunc1Subs refConvolve(IFunc2Subs)
IFunc1Subs refConvolve(IFunc2Subs, boolean, boolean)

// === 卷积（IFunc3Subs 三元完整卷积核） ===
IFunc1 convolveFull(IFunc3Subs)
IFunc1 convolveFull(IFunc3Subs, boolean, boolean)
IFunc1Subs refConvolveFull(IFunc3Subs)
IFunc1Subs refConvolveFull(IFunc3Subs, boolean, boolean)

// === 极值（最大值/最小值位置 x 坐标） ===
double maxX()
double minX()

// === 抽象方法（子类必须实现） ===
protected abstract IFunc1 thisFunc1_()
protected abstract IFunc1 newFunc1_()
```
