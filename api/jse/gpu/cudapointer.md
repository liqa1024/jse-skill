# CudaPointer

> `jse.gpu.CudaPointer`

**核心职能**：`implements ICudaPointer`。GPU 指针的通用实现。`malloc(aCount)` 调用 `CudaCore.cudaMalloc(aCount)`（`TYPE_SIZE=1`，字节数），`free()` 调用 `cudaFree`。提供 `memcpy` D2D/D2H/H2D 重载、`memset`、`copy`（浅拷贝共享同一 GPU 指针）。

```java
@UnsafeJNI static CudaPointer malloc(long aCount) throws CudaException  // cudaMalloc(aCount)
@UnsafeJNI void free() throws CudaException                  // cudaFree + 置零
long typeSize()                                              // 1 (sizeof(char))
static final long TYPE_SIZE = 1

@UnsafeJNI void memcpy2dest(ICudaPointer/ICPointer, long) throws CudaException
@UnsafeJNI void memcpy2this(ICudaPointer/ICPointer, long) throws CudaException
@UnsafeJNI void memset(int aValue, long aCount) throws CudaException

CudaPointer copy()                                                     // 浅拷贝
```
