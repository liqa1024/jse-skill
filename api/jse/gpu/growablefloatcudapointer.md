# GrowableFloatCudaPointer

> `jse.gpu.GrowableFloatCudaPointer`

**核心职能**：`extends FloatCudaPointer`。1.5x 扩容（`cudaFree` 旧 + `cudaMalloc` 新），不保留旧值。

```java
@UnsafeJNI GrowableFloatCudaPointer(long aInitCount) throws CudaException
GrowableFloatCudaPointer()
long count()
void ensureCapacity(long aMinCount) throws CudaException
```
