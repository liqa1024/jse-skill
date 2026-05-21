# GrowableIntCudaPointer

> `jse.gpu.GrowableIntCudaPointer`

**核心职能**：`extends IntCudaPointer`。同 `GrowableFloatCudaPointer`。

```java
@UnsafeJNI GrowableIntCudaPointer(long aInitCount) throws CudaException
GrowableIntCudaPointer()
long count() / void ensureCapacity(long) throws CudaException
```
