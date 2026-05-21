# GrowableInt64CudaPointer

> `jse.gpu.GrowableInt64CudaPointer`

**核心职能**：`extends Int64CudaPointer`。同 `GrowableFloatCudaPointer`。

```java
@UnsafeJNI GrowableInt64CudaPointer(long aInitCount) throws CudaException
GrowableInt64CudaPointer()
long count() / void ensureCapacity(long) throws CudaException
```
