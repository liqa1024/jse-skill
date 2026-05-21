# ILongVectorOperation

> `jse.math.vector.ILongVectorOperation`

**核心职能**：任意的长整数向量运算，包括填充遍历、统计、反转、排序（无算术运算）。

```java
// === 填充与遍历 ===
void fill(long aRHS)
void fill(ILongVector aRHS)
void fill(ILongVectorGetter aRHS)
void assign(LongSupplier aSup)
void forEach(LongConsumer aCon)

// === 统计 ===
long sum()
double mean()
double prod()
long max()
long min()
double stat(DoubleBinaryOperator aOpt)

// === 反转 ===
ILongVector reverse()
ILongVector refReverse()
void reverse2this()
@VisibleForTesting
default ILongVector refreverse()

// === 排序 ===
void sort()
void sort(IntBinaryOperator aComp)
void biSort(ISwapper aSwapper)
void biSort(ISwapper aSwapper, IntBinaryOperator aComp)
@VisibleForTesting
default void bisort(ISwapper aSwapper)
@VisibleForTesting
default void bisort(ISwapper aSwapper, IntBinaryOperator aComp)
```
