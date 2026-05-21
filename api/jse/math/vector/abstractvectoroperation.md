# AbstractVectorOperation

> `jse.math.vector.AbstractVectorOperation`

**核心职能**：`implements IVectorOperation`。实数向量运算的骨架实现。提供全部运算的三种变体 — 返回新向量 (new)、原位修改 (2this)、写入目标 (2dest)，含 `l*` 左变体。`fill`/`assign`/`forEach`、统计归约 + 累积统计、比较运算、dot/norm、reverse、mplus2this (FMA)、sort。子类只需实现 2 个抽象方法，`newLogicalVector_` 有默认实现。

```java
// === 抽象方法（子类须实现） ===
protected abstract IVector thisVector_()
protected abstract IVector newVector_(int aSize)
protected ILogicalVector newLogicalVector_(int aSize)

// === 向量-向量运算（返回新 IVector，final） ===
final IVector plus(IVector aRHS)
final IVector minus(IVector aRHS)
final IVector lminus(IVector aRHS)
final IVector multiply(IVector aRHS)
final IVector div(IVector aRHS)
final IVector ldiv(IVector aRHS)
final IVector mod(IVector aRHS)
final IVector lmod(IVector aRHS)
final IVector operate(IVector aRHS, DoubleBinaryOperator aOpt)

// === 标量运算（返回新 IVector，final） ===
final IVector plus(double aRHS)
final IVector minus(double aRHS)
final IVector lminus(double aRHS)
final IVector multiply(double aRHS)
final IVector div(double aRHS)
final IVector ldiv(double aRHS)
final IVector mod(double aRHS)
final IVector lmod(double aRHS)
final IVector map(DoubleUnaryOperator aOpt)

// === 原位修改 2this（向量） ===
void plus2this(IVector aRHS)
void minus2this(IVector aRHS)
void lminus2this(IVector aRHS)
void multiply2this(IVector aRHS)
void div2this(IVector aRHS)
void ldiv2this(IVector aRHS)
void mod2this(IVector aRHS)
void lmod2this(IVector aRHS)
void operate2this(IVector aRHS, DoubleBinaryOperator aOpt)

// === 原位修改 2this（标量） ===
void plus2this(double aRHS)
void minus2this(double aRHS)
void lminus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)
void ldiv2this(double aRHS)
void mod2this(double aRHS)
void lmod2this(double aRHS)
void map2this(DoubleUnaryOperator aOpt)

// === 写入目标 2dest（向量，写入 IVector rDest） ===
void plus2dest(IVector aRHS, IVector rDest)
void minus2dest(IVector aRHS, IVector rDest)
void lminus2dest(IVector aRHS, IVector rDest)
void multiply2dest(IVector aRHS, IVector rDest)
void div2dest(IVector aRHS, IVector rDest)
void ldiv2dest(IVector aRHS, IVector rDest)
void mod2dest(IVector aRHS, IVector rDest)
void lmod2dest(IVector aRHS, IVector rDest)
void operate2dest(IVector aRHS, IVector rDest, DoubleBinaryOperator aOpt)

// === 写入目标 2dest（标量，写入 IVector rDest） ===
void plus2dest(double aRHS, IVector rDest)
void minus2dest(double aRHS, IVector rDest)
void lminus2dest(double aRHS, IVector rDest)
void multiply2dest(double aRHS, IVector rDest)
void div2dest(double aRHS, IVector rDest)
void ldiv2dest(double aRHS, IVector rDest)
void mod2dest(double aRHS, IVector rDest)
void lmod2dest(double aRHS, IVector rDest)
void map2dest(IVector rDest, DoubleUnaryOperator aOpt)

// === 一元运算 ===
IVector abs()
void abs2this()
IVector negative()
void negative2this()

// === 填充 / 赋值 / 遍历 ===
void fill(double aRHS)
void fill(IVector aRHS)
void fill(IVectorGetter aRHS)
void assign(DoubleSupplier aSup)
void forEach(DoubleConsumer aCon)

// === 统计归约 ===
double sum()
double mean()
double prod()
double max()
double min()
double stat(DoubleBinaryOperator aOpt)

// === 累积统计（返回新 IVector） ===
IVector cumsum()
IVector cummean()
IVector cumprod()
IVector cummax()
IVector cummin()
IVector cumstat(DoubleBinaryOperator aOpt)

// === 比较（返回 ILogicalVector） ===
ILogicalVector equal(IVector aRHS)
ILogicalVector greater(IVector aRHS)
ILogicalVector greaterOrEqual(IVector aRHS)
ILogicalVector less(IVector aRHS)
ILogicalVector lessOrEqual(IVector aRHS)
ILogicalVector equal(double aRHS)
ILogicalVector greater(double aRHS)
ILogicalVector greaterOrEqual(double aRHS)
ILogicalVector less(double aRHS)
ILogicalVector lessOrEqual(double aRHS)
ILogicalVector compare(IVector aRHS, IComparator aOpt)
ILogicalVector check(IChecker aOpt)

// === 向量额外运算 ===
double dot(IVector aRHS)
double dot()
double norm()
double norm1()
IVector reverse()
IVector refReverse()
void reverse2this()
void mplus2this(IVector aRHS, double aMul)

// === 排序 ===
void sort()
void sort(IntBinaryOperator aComp)
void biSort(ISwapper aSwapper)
void biSort(ISwapper aSwapper, IntBinaryOperator aComp)

// === 静态尺寸检查（子类复用，@ApiStatus.Internal） ===
@ApiStatus.Internal static void ebeCheck(int lSize, int rSize)
@ApiStatus.Internal static void ebeCheck(int lSize, int rSize, int dSize)
@ApiStatus.Internal static void mapCheck(int lSize, int dSize)
```
