# IIntVectorOperation

> `jse.math.vector.IIntVectorOperation`

**核心职能**：任意的整数向量运算，包括算术运算、填充遍历、统计、排序、洗牌。

```java
// === 算术运算 (向量) ===
IIntVector plus(IIntVector aRHS)
IIntVector minus(IIntVector aRHS)
IIntVector lminus(IIntVector aRHS)
IIntVector multiply(IIntVector aRHS)
IIntVector div(IIntVector aRHS)
IIntVector ldiv(IIntVector aRHS)
IIntVector mod(IIntVector aRHS)
IIntVector lmod(IIntVector aRHS)
IIntVector operate(IIntVector aRHS, IntBinaryOperator aOpt)

// === 算术运算 (标量) ===
IIntVector plus(int aRHS)
IIntVector minus(int aRHS)
IIntVector lminus(int aRHS)
IIntVector multiply(int aRHS)
IIntVector div(int aRHS)
IIntVector ldiv(int aRHS)
IIntVector mod(int aRHS)
IIntVector lmod(int aRHS)
IIntVector map(IntUnaryOperator aOpt)

// === 原地运算 (向量) ===
void plus2this(IIntVector aRHS)
void minus2this(IIntVector aRHS)
void lminus2this(IIntVector aRHS)
void multiply2this(IIntVector aRHS)
void div2this(IIntVector aRHS)
void ldiv2this(IIntVector aRHS)
void mod2this(IIntVector aRHS)
void lmod2this(IIntVector aRHS)
void operate2this(IIntVector aRHS, IntBinaryOperator aOpt)

// === 原地运算 (标量) ===
void plus2this(int aRHS)
void minus2this(int aRHS)
void lminus2this(int aRHS)
void multiply2this(int aRHS)
void div2this(int aRHS)
void ldiv2this(int aRHS)
void mod2this(int aRHS)
void lmod2this(int aRHS)
void map2this(IntUnaryOperator aOpt)

// === 绝对值与取反 ===
IIntVector abs()
void abs2this()
IIntVector negative()
void negative2this()

// === 填充与遍历 ===
void fill(int aRHS)
void fill(IIntVector aRHS)
void fill(IIntVectorGetter aRHS)
void assign(IntSupplier aSup)
void forEach(IntConsumer aCon)

// === 统计 ===
int sum()
long exsum()
double mean()
double prod()
int max()
int min()
double stat(DoubleBinaryOperator aOpt)

// === 反转 ===
IIntVector reverse()
IIntVector refReverse()
void reverse2this()
@VisibleForTesting
default IIntVector refreverse()

// === 排序 ===
void sort()
void sort(IntBinaryOperator aComp)
void biSort(ISwapper aSwapper)
void biSort(ISwapper aSwapper, IntBinaryOperator aComp)
@VisibleForTesting
default void bisort(ISwapper aSwapper)
@VisibleForTesting
default void bisort(ISwapper aSwapper, IntBinaryOperator aComp)

// === 洗牌 ===
void shuffle()
void shuffle(IRandom aRng)
```
