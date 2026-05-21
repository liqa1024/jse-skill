# FloatCudaPointer

> `jse.gpu.FloatCudaPointer`

**核心职能**：`extends CudaPointer implements IDoubleOrFloatCudaPointer`。GPU 端 `float*`。`typeSize=FloatCPointer.TYPE_SIZE`。

```java
@UnsafeJNI static FloatCudaPointer malloc(long aCount) throws CudaException
// 与 DoubleCudaPointer 镜像，double↔float 互换
@UnsafeJNI void fill(IDataShell<float[]>/float[]/FloatCPointer/FloatCudaPointer) throws CudaException
@UnsafeJNI void fillD(IDataShell<double[]>/double[]/DoubleCPointer) throws CudaException
@UnsafeJNI void parse2dest(IDataShell<float[]>/float[]/FloatCPointer/FloatCudaPointer)
@UnsafeJNI void parse2destD(IDataShell<double[]>/double[]/DoubleCPointer)
FloatCudaPointer copy()
```
