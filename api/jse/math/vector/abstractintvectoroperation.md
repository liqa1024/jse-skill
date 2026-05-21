# AbstractIntVectorOperation

> `jse.math.vector.AbstractIntVectorOperation`

**核心职能**：`implements IIntVectorOperation`。int 向量运算的骨架实现。提供标量/向量算术运算（含 `l*` 左变体）、填充/赋值/遍历、统计归约 (sum/exsum/mean/prod/max/min)、reverse、sort、shuffle。子类只需实现 2 个抽象方法。

```java
// === 抽象方法（子类须实现） ===
protected abstract IIntVector thisVector_()
protected abstract IIntVector newVector_(int aSize)

// === 向量-向量运算（返回新 IIntVector） ===
IIntVector plus(IIntVector aRHS)
IIntVector minus(IIntVector aRHS)
IIntVector lminus(IIntVector aRHS)
IIntVector multiply(IIntVector aRHS)
IIntVector div(IIntVector aRHS)
IIntVector ldiv(IIntVector aRHS)
IIntVector mod(IIntVector aRHS)
IIntVector lmod(IIntVector aRHS)
IIntVector operate(IIntVector aRHS, IntBinaryOperator aOpt)

// === 标量运算（返回新 IIntVector） ===
IIntVector plus(int aRHS)
IIntVector minus(int aRHS)
IIntVector lminus(int aRHS)
IIntVector multiply(int aRHS)
IIntVector div(int aRHS)
IIntVector ldiv(int aRHS)
IIntVector mod(int aRHS)
IIntVector lmod(int aRHS)
IIntVector map(IntUnaryOperator aOpt)

// === 原位修改 2this（向量） ===
void plus2this(IIntVector aRHS)
void minus2this(IIntVector aRHS)
void lminus2this(IIntVector aRHS)
void multiply2this(IIntVector aRHS)
void div2this(IIntVector aRHS)
void ldiv2this(IIntVector aRHS)
void mod2this(IIntVector aRHS)
void lmod2this(IIntVector aRHS)
void operate2this(IIntVector aRHS, IntBinaryOperator aOpt)

// === 原位修改 2this（标量） ===
void plus2this(int aRHS)
void minus2this(int aRHS)
void lminus2this(int aRHS)
void multiply2this(int aRHS)
void div2this(int aRHS)
void ldiv2this(int aRHS)
void mod2this(int aRHS)
void lmod2this(int aRHS)
void map2this(IntUnaryOperator aOpt)

// === 一元运算 ===
IIntVector abs()
void abs2this()
IIntVector negative()
void negative2this()

// === 填充 / 赋值 / 遍历 ===
void fill(int aRHS)
void fill(IIntVector aRHS)
void fill(IIntVectorGetter aRHS)
void assign(IntSupplier aSup)
void forEach(IntConsumer aCon)

// === 统计归约 ===
int sum()
long exsum()
double mean()
double prod()
int max()
int min()
double stat(DoubleBinaryOperator aOpt)

// === 向量额外运算 ===
IIntVector reverse()
IIntVector refReverse()
void reverse2this()

// === 排序 ===
void sort()
void sort(IntBinaryOperator aComp)
void biSort(ISwapper aSwapper)
void biSort(ISwapper aSwapper, IntBinaryOperator aComp)

// === 乱序 ===
final void shuffle()
void shuffle(IRandom aRng)
```
