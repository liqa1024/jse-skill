# DoubleArrayVectorOperation

> `jse.math.vector.DoubleArrayVectorOperation`

**核心职能**：`abstract class extends AbstractVectorOperation`。面向 `DoubleArrayVector` 的运算优化层，采用 ARRAY（直接 `double[]` 访问）与 DATA（迭代器回退）双路径策略：若 RHS 同样为同序 `IDataShell<double[]>` 则走 ARRAY 路径，否则回退 DATA。

```java
// === 向量-向量运算（原位修改） ===
void plus2this(IVector)
void minus2this(IVector)
void lminus2this(IVector)
void multiply2this(IVector)
void div2this(IVector)
void ldiv2this(IVector)
void mod2this(IVector)
void lmod2this(IVector)
void operate2this(IVector, DoubleBinaryOperator)

// === 标量运算（原位修改） ===
void plus2this(double)
void minus2this(double)
void lminus2this(double)
void multiply2this(double)
void div2this(double)
void ldiv2this(double)
void mod2this(double)
void lmod2this(double)
void map2this(DoubleUnaryOperator)

// === 一元运算 ===
IVector abs()
void abs2this()
IVector negative()
void negative2this()

// === 向量-向量运算（写入目标） ===
void plus2dest(IVector, IVector rDest)
void minus2dest(IVector, IVector rDest)
void lminus2dest(IVector, IVector rDest)
void multiply2dest(IVector, IVector rDest)
void div2dest(IVector, IVector rDest)
void ldiv2dest(IVector, IVector rDest)
void mod2dest(IVector, IVector rDest)
void lmod2dest(IVector, IVector rDest)
void operate2dest(IVector, IVector rDest, DoubleBinaryOperator)

// === 标量运算（写入目标） ===
void plus2dest(double, IVector rDest)
void minus2dest(double, IVector rDest)
void lminus2dest(double, IVector rDest)
void multiply2dest(double, IVector rDest)
void div2dest(double, IVector rDest)
void ldiv2dest(double, IVector rDest)
void mod2dest(double, IVector rDest)
void lmod2dest(double, IVector rDest)
void map2dest(IVector rDest, DoubleUnaryOperator)

// === 填充 / 赋值 / 遍历 ===
void fill(double/IVector/IVectorGetter)
void assign(DoubleSupplier)
void forEach(DoubleConsumer)

// === 统计 ===
double sum()
double mean()
double prod()
double max()
double min()
double stat(DoubleBinaryOperator)

// === 向量额外 ===
double dot(IVector)
double dot()
double norm1()
IVector reverse()
void mplus2this(IVector, double)
void sort()
void biSort(ISwapper)

// === 子类需实现 ===
protected abstract DoubleArrayVector thisVector_()
protected abstract DoubleArrayVector newVector_(int aSize)
```
