# Int64CudaPointer

> `jse.gpu.Int64CudaPointer`

**核心职能**：`extends CudaPointer`。GPU 端 `int64_t*`。`typeSize=Int64CPointer.TYPE_SIZE`。支持 fill/parse2dest 于 `IDataShell<long[]>`/`long[]`/`Int64CPointer`/`Int64CudaPointer`。

```java
@UnsafeJNI static Int64CudaPointer malloc(long aCount) throws CudaException
@UnsafeJNI void fill(IDataShell<long[]>/long[]/Int64CPointer/Int64CudaPointer) throws CudaException
@UnsafeJNI void parse2dest(IDataShell<long[]>/long[]/Int64CPointer/Int64CudaPointer)
Int64CudaPointer copy()
```
