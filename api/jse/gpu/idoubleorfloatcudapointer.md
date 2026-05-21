# IDoubleOrFloatCudaPointer

> `jse.gpu.IDoubleOrFloatCudaPointer`

**核心职能**：extends ICudaPointer（`@ApiStatus.Experimental`）。与 `jse.cptr.IDoubleOrFloatCPointer` 镜像，统一 double/float GPU 指针的批量读写（`fillD`/`fillF`、`parse2destD`/`parse2destF`），支持 `IDataShell`/数组/`CPointer` 多种数据源。**无** `get`/`set`/`getAt`/`putAt` 单元素访问（GPU 不适合逐元素操作）。

```java
@UnsafeJNI void fillD(IDataShell<double[]>/double[] aData,...) throws CudaException
@UnsafeJNI void fillF(IDataShell<float[]>/float[] aData,...) throws CudaException
@UnsafeJNI void fillD(DoubleCPointer aData, long aCount) throws CudaException
@UnsafeJNI void fillF(FloatCPointer aData, long aCount) throws CudaException
@UnsafeJNI void parse2destD(IDataShell<double[]>/double[] rDest,...)
@UnsafeJNI void parse2destF(IDataShell<float[]>/float[] rDest,...)
@UnsafeJNI void parse2destD(DoubleCPointer rDest, long aCount) throws CudaException
@UnsafeJNI void parse2destF(FloatCPointer rDest, long aCount) throws CudaException
```
