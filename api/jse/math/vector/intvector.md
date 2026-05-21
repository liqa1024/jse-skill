# IntVector

> `jse.math.vector.IntVector`

**核心职能**：`final class extends IntArrayVector`。int 类型向量的具体实现，支持 `mShift` 零拷贝切片（`subVec`）。提供 `builder()` 进行构造期动态追加，Builder 详见 [intvector_builder.md](intvector_builder.md)。

```java
// === 静态工厂 ===
static IntVector zeros(int aSize)
static IntVector ones(int aSize)
static Builder builder()
static Builder builder(int aInitSize)

// === 构造 ===
IntVector(int[] aData)
IntVector(int aSize, int[] aData)
IntVector(int aSize, int aShift, int[] aData)

// === 内部参数 ===
void setInternalDataSize(int aSize)
void setInternalDataShift(int aShift)
int internalDataShift()

// === IIntVector ===
int get(int aIdx)
void set(int aIdx, int aValue)
int getAndSet(int aIdx, int aValue)
int size()

// === 批量 ===
IntVector copy()
IntVector subVec(int aFromIdx, int aToIdx)
int @Nullable[] getIfHasSameOrderData(Object aObj)

// === numpy 零拷贝 ===
NDArray<int[]> numpy()

// === 高级索引 ===
void swap(int aIdx1, int aIdx2)
void increment(int aIdx)
int getAndIncrement(int aIdx)
void decrement(int aIdx)
int getAndDecrement(int aIdx)
void add(int aIdx, int aDelta)
int getAndAdd(int aIdx, int aDelta)
void update(int aIdx, IntUnaryOperator)
int getAndUpdate(int aIdx, IntUnaryOperator)

// === 查询 ===
boolean isEmpty()
int last()
int first()

// === 迭代器 ===
IIntIterator iterator()
IIntSetIterator setIterator()
```
