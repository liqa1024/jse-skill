# IntCudaPointer

> `jse.gpu.IntCudaPointer`

**核心职能**：`extends CudaPointer`。GPU 端 `int*`。`typeSize=IntCPointer.TYPE_SIZE`。支持 fill/parse2dest 于 `IDataShell<int[]>`/`int[]`/`IntCPointer`/`IntCudaPointer`。

```java
@UnsafeJNI static IntCudaPointer malloc(long aCount) throws CudaException
@UnsafeJNI void fill(IDataShell<int[]>/int[]/IntCPointer/IntCudaPointer) throws CudaException
@UnsafeJNI void parse2dest(IDataShell<int[]>/int[]/IntCPointer/IntCudaPointer)
IntCudaPointer copy()
```
