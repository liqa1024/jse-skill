# IFunc1Operation

> `jse.math.function.IFunc1Operation`

**核心职能**：一维函数的各类运算：函数间/标量二元运算、带坐标运算、填充遍历、微分积分、卷积、极值。

```java
// === 函数间二元运算（返回新 IFunc1） ===
IFunc1 plus(IFunc1 aRHS)
IFunc1 minus(IFunc1 aRHS)
IFunc1 lminus(IFunc1 aRHS)
IFunc1 multiply(IFunc1 aRHS)
IFunc1 div(IFunc1 aRHS)
IFunc1 ldiv(IFunc1 aRHS)
IFunc1 mod(IFunc1 aRHS)
IFunc1 lmod(IFunc1 aRHS)
IFunc1 operate(IFunc1 aRHS, DoubleBinaryOperator aOpt)

// --- 原地修改 ---
void plus2this(IFunc1 aRHS)
void minus2this(IFunc1 aRHS)
void lminus2this(IFunc1 aRHS)
void multiply2this(IFunc1 aRHS)
void div2this(IFunc1 aRHS)
void ldiv2this(IFunc1 aRHS)
void mod2this(IFunc1 aRHS)
void lmod2this(IFunc1 aRHS)
void operate2this(IFunc1 aRHS, DoubleBinaryOperator aOpt)

// === 标量运算 ===
IFunc1 plus(double aRHS)
IFunc1 minus(double aRHS)
IFunc1 lminus(double aRHS)
IFunc1 multiply(double aRHS)
IFunc1 div(double aRHS)
IFunc1 ldiv(double aRHS)
IFunc1 mod(double aRHS)
IFunc1 lmod(double aRHS)
IFunc1 map(DoubleUnaryOperator aOpt)

// --- 原地修改 ---
void plus2this(double aRHS)
void minus2this(double aRHS)
void lminus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)
void ldiv2this(double aRHS)
void mod2this(double aRHS)
void lmod2this(double aRHS)
void map2this(DoubleUnaryOperator aOpt)

// === 填充与遍历 ===
void fill(double aRHS)
void fill(IVector aRHS)
void fill(IFunc1 aRHS)
void fill(IFunc1Subs aRHS)
void assign(DoubleSupplier aSup)
void forEach(DoubleConsumer aCon)

// === 带坐标运算（传入 f+rhs+x 三元 / f+x 二元） ===
IFunc1 operateFull(IFunc1 aRHS, IDoubleTernaryOperator aOpt)
IFunc1 mapFull(DoubleBinaryOperator aOpt)
void operateFull2this(IFunc1 aRHS, IDoubleTernaryOperator aOpt)
void mapFull2this(DoubleBinaryOperator aOpt)

// === 微分（有限差分中心差分） ===
IFunc1 gradient()
IFunc1 gradient(boolean aConsiderBound)
IFunc1 laplacian()
IFunc1 laplacian(boolean aConsiderBound)

// === 积分（梯形法） ===
double integral()
double integral(boolean aConsiderBoundL, boolean aConsiderBoundR)

// === 卷积 ===
IFunc1 convolve(IFunc2Subs aConv)
IFunc1 convolve(IFunc2Subs aConv, boolean aConsiderBoundL, boolean aConsiderBoundR)
IFunc1Subs refConvolve(IFunc2Subs aConv)
IFunc1Subs refConvolve(IFunc2Subs aConv, boolean aConsiderBoundL, boolean aConsiderBoundR)
IFunc1 convolveFull(IFunc3Subs aConv)
IFunc1 convolveFull(IFunc3Subs aConv, boolean aConsiderBoundL, boolean aConsiderBoundR)
IFunc1Subs refConvolveFull(IFunc3Subs aConv)
IFunc1Subs refConvolveFull(IFunc3Subs aConv, boolean aConsiderBoundL, boolean aConsiderBoundR)

// === 极值 ===
double maxX()
double minX()
```
