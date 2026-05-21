# AbstractLongVectorOperation

> `jse.math.vector.AbstractLongVectorOperation`

**核心职能**：长整型向量的运算骨架，实现 `ILongVectorOperation`。提供填充/赋值/遍历、统计（sum/mean/prod/max/min/stat）、反向、排序等操作的默认实现。继承需实现 `thisVector_`/`newVector_`。

```java
// === 填充/赋值/遍历 ===
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

// === 反向 ===
ILongVector reverse()
ILongVector refReverse()
void reverse2this()

// === 排序 ===
void sort()
void sort(IntBinaryOperator aComp)
void biSort(ISwapper aSwapper)
void biSort(ISwapper aSwapper, IntBinaryOperator aComp)

// === 子类需实现 ===
protected abstract ILongVector thisVector_()
protected abstract ILongVector newVector_(int aSize)
```
