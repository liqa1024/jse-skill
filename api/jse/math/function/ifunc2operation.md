# IFunc2Operation

> `jse.math.function.IFunc2Operation`

**核心职能**：二维函数的各类运算：函数间/标量二元运算、带坐标运算、填充。

```java
// === 函数间二元运算 ===
IFunc2 plus(IFunc2 aRHS)
IFunc2 minus(IFunc2 aRHS)
IFunc2 lminus(IFunc2 aRHS)
IFunc2 multiply(IFunc2 aRHS)
IFunc2 div(IFunc2 aRHS)
IFunc2 ldiv(IFunc2 aRHS)
IFunc2 mod(IFunc2 aRHS)
IFunc2 lmod(IFunc2 aRHS)
IFunc2 operate(IFunc2 aRHS, DoubleBinaryOperator aOpt)

// --- 原地修改 ---
void plus2this(IFunc2 aRHS)
void minus2this(IFunc2 aRHS)
void lminus2this(IFunc2 aRHS)
void multiply2this(IFunc2 aRHS)
void div2this(IFunc2 aRHS)
void ldiv2this(IFunc2 aRHS)
void mod2this(IFunc2 aRHS)
void lmod2this(IFunc2 aRHS)
void operate2this(IFunc2 aRHS, DoubleBinaryOperator aOpt)

// === 标量运算 ===
IFunc2 plus(double aRHS)
IFunc2 minus(double aRHS)
IFunc2 lminus(double aRHS)
IFunc2 multiply(double aRHS)
IFunc2 div(double aRHS)
IFunc2 ldiv(double aRHS)
IFunc2 mod(double aRHS)
IFunc2 lmod(double aRHS)
IFunc2 map(DoubleUnaryOperator aOpt)

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

// === 填充 ===
void fill(double aValue)
void fill(IMatrix aMatrix)
void fill(IFunc2 aFunc2)
void fill(IFunc2Subs aFunc2Subs)

// === 带坐标运算（四元: f+rhs+x+y / 三元: f+x+y） ===
IFunc2 operateFull(IFunc2 aRHS, IDoubleQuaternionOperator aOpt)
IFunc2 mapFull(IDoubleTernaryOperator aOpt)
void operateFull2this(IFunc2 aRHS, IDoubleQuaternionOperator aOpt)
void mapFull2this(IDoubleTernaryOperator aOpt)
```
