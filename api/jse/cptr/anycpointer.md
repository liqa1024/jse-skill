# AnyCPointer

> `jse.cptr.AnyCPointer`

**核心职能**：`extends CPointer`。对应 C 的 `void **`。通过 `get()` 解引用得 `IPointer`，`getAs*Pointer()` 解引用同时类型转换。提供 `getAt`/`putAt` 按索引访问内部指针数组，`asList` 转为列表视图。**覆写了全部指针算术**。

```java
// --- 解引用 (*ptr → IPointer 或指定类型) ---
@UnsafeJNI IPointer get()                            // *ptr → Pointer
@UnsafeJNI CPointer getAsCPointer()                  // (char *)*ptr
@UnsafeJNI DoubleCPointer getAsDoubleCPointer()      // (double *)*ptr
@UnsafeJNI FloatCPointer getAsFloatCPointer()
@UnsafeJNI IntCPointer getAsIntCPointer()
@UnsafeJNI AnyCPointer getAsAnyCPointer()            // (void **)*ptr
@UnsafeJNI CudaPointer getAsCudaPointer() / getAsIntCudaPointer() / getAsFloatCudaPointer() / getAsDoubleCudaPointer()

// --- 数组索引 (ptr[aIdx]) ---
@UnsafeJNI IPointer getAt(long aIdx) / getAt(int aIdx)  // Groovy 兼容
@UnsafeJNI CPointer/DoubleCPointer/FloatCPointer/IntCPointer/AnyCPointer/CudaPointer/...
        getAs*PointerAt(long aIdx)

// --- 写入 ---
@UnsafeJNI void set(@NotNull IPointer aValue)        // *ptr = aValue
@UnsafeJNI void putAt(long aIdx, @NotNull IPointer aValue)  // ptr[aIdx] = aValue

// --- 批量 ---
@UnsafeJNI void fill(AnyCPointer aData, long aCount)        // memcpy(len=aCount*TYPE_SIZE)
@UnsafeJNI void parse2dest(AnyCPointer rDest, long aCount)

// --- 指针算术 (覆写) ---
void next/previous/rightShift/leftShift(...)
AnyCPointer plus/minus(long aCount)

// --- 视图 ---
@UnsafeJNI List<? extends IPointer> asList(int aSize)  // 指针数组引用视图

static AnyCPointer malloc/calloc(long aCount)
static final long TYPE_SIZE = typeSize0()               // sizeof(void *)
```
