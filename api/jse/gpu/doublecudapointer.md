# DoubleCudaPointer

> `jse.gpu.DoubleCudaPointer`

**核心职能**：`extends CudaPointer implements IDoubleOrFloatCudaPointer`。GPU 端 `double*`。与 `DoubleCPointer` 镜像但操作 GPU 显存。提供 `fill`/`parse2dest`（IDataShell/double[]/DoubleCPointer/DoubleCudaPointer）+ 跨精度 `fillF`/`parse2destF`。**无** `get`/`set`/`getAt`/`putAt`。`typeSize=TYPE_SIZE`（`DoubleCPointer.TYPE_SIZE`）。

```java
@UnsafeJNI static DoubleCudaPointer malloc(long aCount) throws CudaException

// --- 填充 (H→D) ---
@UnsafeJNI void fill(IDataShell<double[]> aData) throws CudaException
@UnsafeJNI void fill(double[] aData, int aStart, int aCount) throws CudaException
@UnsafeJNI void fill(DoubleCPointer aData, long aCount) throws CudaException    // H2D
@UnsafeJNI void fill(DoubleCudaPointer aData, long aCount) throws CudaException  // D2D

// --- 跨精度 (float→double*) ---
@UnsafeJNI void fillF(IDataShell<float[]>/float[]/FloatCPointer) throws CudaException

// --- 解析 (D→H) ---
@UnsafeJNI void parse2dest(IDataShell<double[]> rDest)
@UnsafeJNI void parse2dest(double[] rDest, int aStart, int aCount)
@UnsafeJNI void parse2dest(DoubleCPointer rDest, long aCount) throws CudaException
@UnsafeJNI void parse2dest(DoubleCudaPointer rDest, long aCount) throws CudaException

// --- 跨精度解析 (double*→float) ---
@UnsafeJNI void parse2destF(IDataShell<float[]>/float[]/FloatCPointer)

DoubleCudaPointer copy()
```
