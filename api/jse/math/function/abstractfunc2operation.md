# AbstractFunc2Operation

> `jse.math.function.AbstractFunc2Operation`

> 此类标记为 @ApiStatus.Experimental

**核心职能**：二维函数运算器抽象骨架。`abstract class implements IFunc2Operation`。提供二元运算、标量运算、带坐标运算的默认实现。**注意：无 gradient/laplacian/integral/convolve（仅一维有）。**

```java
// === 函数间二元运算（返回新 IFunc2） ===
IFunc2 plus/minus/lminus/multiply/div/ldiv/mod/lmod(IFunc2)
IFunc2 operate(IFunc2, DoubleBinaryOperator)

// === 原地二元运算（修改自身） ===
void plus2this/minus2this/lminus2this/multiply2this/div2this/ldiv2this/mod2this/lmod2this(IFunc2)
void operate2this(IFunc2, DoubleBinaryOperator)

// === 标量二元运算（返回新 IFunc2） ===
IFunc2 plus/minus/lminus/multiply/div/ldiv/mod/lmod(double)
IFunc2 map(DoubleUnaryOperator)

// === 标量原地运算 ===
void plus2this/minus2this/lminus2this/multiply2this/div2this/ldiv2this/mod2this/lmod2this(double)
void map2this(DoubleUnaryOperator)

// === fill ===
void fill(double)
void fill(IMatrix)
void fill(IFunc2)
void fill(IFunc2Subs)

// === 带坐标运算（四元: f+rhs+x+y / 三元: f+x+y） ===
IFunc2 operateFull(IFunc2, IDoubleQuaternionOperator)
IFunc2 mapFull(IDoubleTernaryOperator)
void operateFull2this(IFunc2, IDoubleQuaternionOperator)
void mapFull2this(IDoubleTernaryOperator)

// === 抽象方法（子类必须实现） ===
protected abstract IFunc2 thisFunc2_()
protected abstract IFunc2 newFunc2_()
```
