# CPointer

> `jse.cptr.CPointer`

**核心职能**：`implements ICPointer`。所有类型化 C 指针的基类。提供 JNI 库编译（cpointer）、`malloc`/`calloc`/`free`、`memcpy`。`typeSize()=1` (sizeof(char))。**指针算术默认抛 `UnsupportedOperationException`**，由子类覆写。`NULL` / `nullptr` 常量（空指针单例）。构造器 `@ApiStatus.Internal`，通过子类静态工厂获取实例。

```java
static class InitHelper {
    static boolean initialized()
    static void init()
}
static class Conf {
    static final Map<String, String> CMAKE_SETTING     // JSE_CMAKE_SETTING_CPOINTER
    static @Nullable String CMAKE_C_COMPILER / CXX_COMPILER / C_FLAGS / CXX_FLAGS
    static boolean USE_MIMALLOC                         // 是否用 MiMalloc (默认 true, JSE_USE_MIMALLOC_CPOINTER)
}

// === 静态常量 ===
static final String LIB_DIR / LIB_PATH
static final IPointer NULL / nullptr                // 空指针单例 (ptr_()=0, isNull()=true)
static final long TYPE_SIZE = 1                     // sizeof(char)

// === 内存分配 (静态工厂) ===
@UnsafeJNI static CPointer malloc(long aCount)      // malloc(aCount * TYPE_SIZE)
@UnsafeJNI static CPointer calloc(long aCount)      // calloc(aCount, TYPE_SIZE)
@UnsafeJNI void free()
@UnsafeJNI void memcpy2dest/memcpy2this(...)

// === 指针算术 (默认 UnsupportedOperationException) ===
void next/previous/rightShift/leftShift(...)
CPointer plus/minus(long aCount)
CPointer copy()
```
