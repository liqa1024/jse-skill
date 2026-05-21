# LongVector

> `jse.math.vector.LongVector`

**核心职能**：`final class extends LongArrayVector`。long 类型向量的 final 具体实现，支持 `mShift` 零拷贝切片（`subVec`）。提供静态工厂方法和 Builder 进行构造期动态追加，Builder 详见 [longvector_builder.md](longvector_builder.md)。

```java
// === 静态工厂 ===
static LongVector zeros(int aSize)
static LongVector ones(int aSize)
static Builder builder()
static Builder builder(int aInitSize)

// === 构造 ===
LongVector(long[] aData)
LongVector(int aSize, long[] aData)
LongVector(int aSize, int aShift, long[] aData)

// === IDataShell ===
void setInternalDataSize(int aSize)
void setInternalDataShift(int aShift)

// === 元素访问 ===
final int size()
final long get(int aIdx)
final void set(int aIdx, long aValue)
final long getAndSet(int aIdx, long aValue)
final boolean isEmpty()
final long last()
final long first()

// === 单元素原子操作 ===
final void increment(int aIdx)
final long getAndIncrement(int aIdx)
final void decrement(int aIdx)
final long getAndDecrement(int aIdx)
final void add(int aIdx, long aDelta)
final long getAndAdd(int aIdx, long aDelta)
final void update(int aIdx, LongUnaryOperator aOpt)
final long getAndUpdate(int aIdx, LongUnaryOperator aOpt)

// === 交换 ===
final void swap(int aIdx1, int aIdx2)

// === 切片与拷贝 ===
final LongVector subVec(int aFromIdx, int aToIdx)
final LongVector copy()

// === 转换 ===
final NDArray<long[]> numpy()
final int internalDataShift()
final long @Nullable[] getIfHasSameOrderData(Object aObj)

// === 迭代器 ===
final ILongIterator iterator()
final ILongSetIterator setIterator()
```
