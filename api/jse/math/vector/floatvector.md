# FloatVector

> `jse.math.vector.FloatVector`

**核心职能**：`final class extends FloatArrayVector`。float 类型向量的具体实现，支持 `mShift` 零拷贝切片（`subVec`）。提供 `builder()` 进行构造期动态追加，Builder 详见 [floatvector_builder.md](floatvector_builder.md)。

```java
// === 静态工厂 ===
static FloatVector zeros(int aSize)
static FloatVector ones(int aSize)
static Builder builder()
static Builder builder(int aInitSize)

// === 构造 ===
FloatVector(float[] aData)
FloatVector(int aSize, float[] aData)
FloatVector(int aSize, int aShift, float[] aData)

// === 内部参数 ===
void setInternalDataSize(int aSize)
void setInternalDataShift(int aShift)
int internalDataShift()

// === IFloatVector ===
float get(int aIdx)
void set(int aIdx, float aValue)
float getAndSet(int aIdx, float aValue)
int size()

// === 批量 ===
FloatVector copy()
FloatVector subVec(int aFromIdx, int aToIdx)
float @Nullable[] getIfHasSameOrderData(Object aObj)

// === numpy 零拷贝 ===
NDArray<float[]> numpy()

// === 高级索引 ===
void swap(int aIdx1, int aIdx2)
void update(int aIdx, IFloatUnaryOperator)
float getAndUpdate(int aIdx, IFloatUnaryOperator)

// === 查询 ===
boolean isEmpty()
float last()
float first()

// === 迭代器 ===
IFloatIterator iterator()
IFloatSetIterator setIterator()
```
