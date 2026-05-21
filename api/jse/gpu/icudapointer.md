# ICudaPointer

> `jse.gpu.ICudaPointer`

**核心职能**：extends IPointer（`@ApiStatus.Experimental`）。定义 GPU 显存指针的生命周期：`free`（调用 `cudaFree`）、`memcpy2dest/2this`（D2D + D2H/H2D 双重重载）、`memset`（调用 `cudaMemset`）、`typeSize`。

```java
@UnsafeJNI void free() throws CudaException                         // cudaFree
@UnsafeJNI void memcpy2dest(ICudaPointer rDest, long aCount) throws CudaException  // D2D
@UnsafeJNI void memcpy2dest(ICPointer rDest, long aCount) throws CudaException     // D2H
@UnsafeJNI void memcpy2this(ICudaPointer aSrc, long aCount) throws CudaException   // D2D
@UnsafeJNI void memcpy2this(ICPointer aSrc, long aCount) throws CudaException      // H2D
@UnsafeJNI void memset(int aValue, long aCount) throws CudaException  // cudaMemset
long typeSize()                                                      // sizeof(type)
```
