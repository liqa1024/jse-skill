# LogicalVector

> `jse.math.vector.LogicalVector`

**核心职能**：`final class extends BooleanArrayVector`。boolean 类型（逻辑）向量的 final 具体实现，支持 `mShift` 零拷贝切片（`subVec`）。提供静态工厂方法和 Builder 进行构造期动态追加，Builder 详见 [logicalvector_builder.md](logicalvector_builder.md)。

```java
// === 静态工厂 ===
static LogicalVector zeros(int aSize)
static LogicalVector ones(int aSize)
static Builder builder()
static Builder builder(int aInitSize)

// === 构造 ===
LogicalVector(boolean[] aData)
LogicalVector(int aSize, boolean[] aData)
LogicalVector(int aSize, int aShift, boolean[] aData)

// === IDataShell ===
void setInternalDataSize(int aSize)
void setInternalDataShift(int aShift)

// === 元素访问 ===
final int size()
final boolean get(int aIdx)
final void set(int aIdx, boolean aValue)
final boolean getAndSet(int aIdx, boolean aValue)
final boolean isEmpty()
final boolean last()
final boolean first()

// === 单元素原子操作 ===
final void flip(int aIdx)
final boolean getAndFlip(int aIdx)
final void update(int aIdx, IBooleanUnaryOperator aOpt)
final boolean getAndUpdate(int aIdx, IBooleanUnaryOperator aOpt)

// === 交换 ===
final void swap(int aIdx1, int aIdx2)

// === 切片与拷贝 ===
final LogicalVector subVec(int aFromIdx, int aToIdx)
final LogicalVector copy()

// === 转换 ===
final NDArray<boolean[]> numpy()
final int internalDataShift()
final boolean @Nullable[] getIfHasSameOrderData(Object aObj)

// === 迭代器 ===
final IBooleanIterator iterator()
final IBooleanSetIterator setIterator()
```
