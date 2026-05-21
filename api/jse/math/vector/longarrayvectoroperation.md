# LongArrayVectorOperation

> `jse.math.vector.LongArrayVectorOperation`

**核心职能**：`extends AbstractLongVectorOperation`。long 类型向量的 ARRAY/DATA 双路径运算实现。优先尝试直接操作 `long[]` 底层数组（ARRAY 路径），不兼容时回退至接口调用（DATA 路径）。

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

// === 排序 ===
void sort()
void biSort(ISwapper aSwapper)

// === 子类需实现 ===
protected abstract LongArrayVector thisVector_()
protected abstract LongArrayVector newVector_(int aSize)
```
