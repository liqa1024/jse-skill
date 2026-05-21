# IntArrayVectorOperation

> `jse.math.vector.IntArrayVectorOperation`

**核心职能**：`abstract class extends AbstractIntVectorOperation`。面向 `IntArrayVector` 的运算优化层，ARRAY/DATA 双路径覆盖全部向量-向量及标量运算。

```java
// === 向量-向量运算（返回新向量） ===
IIntVector plus(IIntVector)
IIntVector minus(IIntVector)
IIntVector lminus(IIntVector)
IIntVector multiply(IIntVector)
IIntVector div(IIntVector)
IIntVector ldiv(IIntVector)
IIntVector mod(IIntVector)
IIntVector lmod(IIntVector)
IIntVector operate(IIntVector, IntBinaryOperator)

// === 标量运算（返回新向量） ===
IIntVector plus(int)
IIntVector minus(int)
IIntVector lminus(int)
IIntVector multiply(int)
IIntVector div(int)
IIntVector ldiv(int)
IIntVector mod(int)
IIntVector lmod(int)
IIntVector map(IntUnaryOperator)

// === 向量-向量运算（原位修改） ===
void plus2this(IIntVector)
void minus2this(IIntVector)
void lminus2this(IIntVector)
void multiply2this(IIntVector)
void div2this(IIntVector)
void ldiv2this(IIntVector)
void mod2this(IIntVector)
void lmod2this(IIntVector)
void operate2this(IIntVector, IntBinaryOperator)

// === 标量运算（原位修改） ===
void plus2this(int)
void minus2this(int)
void lminus2this(int)
void multiply2this(int)
void div2this(int)
void ldiv2this(int)
void mod2this(int)
void lmod2this(int)
void map2this(IntUnaryOperator)

// === 一元运算 ===
IIntVector abs()
void abs2this()
IIntVector negative()
void negative2this()

// === 填充 / 赋值 / 遍历 ===
void fill(int/IIntVector/IIntVectorGetter)
void assign(IntSupplier)
void forEach(IntConsumer)

// === 统计 ===
int sum()
long exsum()
double mean()
double prod()
int max()
int min()
double stat(DoubleBinaryOperator)

// === 向量额外 ===
IIntVector reverse()
void sort()
void biSort(ISwapper)

// === 子类需实现 ===
protected abstract IntArrayVector thisVector_()
protected abstract IntArrayVector newVector_(int aSize)
```
