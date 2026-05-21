# IVectorOperation

> `jse.math.vector.IVectorOperation`

**核心职能**：分离式运算接口，提供全部运算的三种变体 — 返回新向量、原位修改 (2this)、写入目标 (2dest)。

```java
// === 向量-向量运算 ===
// 返回新向量: plus, minus, lminus, multiply, div, ldiv, mod, lmod
IVector plus(IVector)
IVector minus(IVector)
IVector lminus(IVector)
IVector multiply(IVector)
IVector div(IVector)
IVector ldiv(IVector)
IVector mod(IVector)
IVector lmod(IVector)
IVector operate(IVector, DoubleBinaryOperator)
// 原位修改: plus2this, minus2this, lminus2this, multiply2this, div2this, ldiv2this, mod2this, lmod2this
void plus2this(IVector)
void minus2this(IVector)
void lminus2this(IVector)
void multiply2this(IVector)
void div2this(IVector)
void ldiv2this(IVector)
void mod2this(IVector)
void lmod2this(IVector)
void operate2this(IVector, DoubleBinaryOperator)
// 写入目标: plus2dest, minus2dest, lminus2dest, multiply2dest, div2dest, ldiv2dest, mod2dest, lmod2dest
void plus2dest(IVector, IVector rDest)
void minus2dest(IVector, IVector rDest)
void lminus2dest(IVector, IVector rDest)
void multiply2dest(IVector, IVector rDest)
void div2dest(IVector, IVector rDest)
void ldiv2dest(IVector, IVector rDest)
void mod2dest(IVector, IVector rDest)
void lmod2dest(IVector, IVector rDest)

// === 标量运算 ===
// 返回新向量: plus, minus, lminus, multiply, div, ldiv, mod, lmod
IVector plus(double)
IVector minus(double)
IVector lminus(double)
IVector multiply(double)
IVector div(double)
IVector ldiv(double)
IVector mod(double)
IVector lmod(double)
IVector map(DoubleUnaryOperator)
// 原位修改: plus2this, minus2this, lminus2this, multiply2this, div2this, ldiv2this, mod2this, lmod2this
void plus2this(double)
void minus2this(double)
void lminus2this(double)
void multiply2this(double)
void div2this(double)
void ldiv2this(double)
void mod2this(double)
void lmod2this(double)
void map2this(DoubleUnaryOperator)
// 写入目标: plus2dest, minus2dest, lminus2dest, multiply2dest, div2dest, ldiv2dest, mod2dest, lmod2dest
void plus2dest(double, IVector rDest)
void minus2dest(double, IVector rDest)
void lminus2dest(double, IVector rDest)
void multiply2dest(double, IVector rDest)
void div2dest(double, IVector rDest)
void ldiv2dest(double, IVector rDest)
void mod2dest(double, IVector rDest)
void lmod2dest(double, IVector rDest)
void map2dest(IVector rDest, DoubleUnaryOperator)

// === 一元 ===
IVector abs()
void abs2this()
IVector negative()
void negative2this()

// === 填充/赋值/遍历 ===
void fill(double/IVector/IVectorGetter)
void assign(DoubleSupplier)
void forEach(DoubleConsumer)

// === 统计（归约 + 累积） ===
double sum()
double mean()
double prod()
double max()
double min()
double stat(DoubleBinaryOperator)
IVector cumsum()
IVector cummean()
IVector cumprod()
IVector cummax()
IVector cummin()
IVector cumstat(DoubleBinaryOperator)

// === 比较 ===
ILogicalVector equal(IVector/double)
ILogicalVector greater(IVector/double)
ILogicalVector greaterOrEqual(IVector/double)
ILogicalVector less(IVector/double)
ILogicalVector lessOrEqual(IVector/double)
ILogicalVector compare(IVector, IComparator)
ILogicalVector check(IChecker)

// === 向量额外 ===
double dot(IVector)
double dot()
double norm()
double norm1()
IVector reverse()
IVector refReverse()
void reverse2this()
void mplus2this(IVector, double)                   // this += aRHS * aMul (FMA)
void sort()
void sort(IntBinaryOperator)
void biSort(ISwapper)
void biSort(ISwapper, IntBinaryOperator)
```
