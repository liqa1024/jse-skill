# `jse.gpu`

> CUDA GPU 指针包装——与 `jse.cptr` 镜像的 GPU 显存管理。提供 `cudaMalloc`/`cudaFree`/`cudaMemcpy(D2D/D2H/H2D)`/`cudaMemset`。`CudaCore` 封装 CUDA Runtime API 的 JNI 转发，`CudaJIT` 支持运行时编译 `.cu` 核函数。整个包标注 `@ApiStatus.Experimental`。

## 架构总览 (Architecture)

```
ICudaPointer extends IPointer (@Experimental)
  → IDoubleOrFloatCudaPointer (@Experimental)

CudaPointer implements ICudaPointer           — GPU 指针基类, sizeof(char)=1
  → DoubleCudaPointer + IDoubleOrFloatCudaPointer  — double* GPU
    → (无 GrowableDoubleCudaPointer)
  → FloatCudaPointer + IDoubleOrFloatCudaPointer   — float* GPU
    → GrowableFloatCudaPointer
  → IntCudaPointer                                 — int* GPU
    → GrowableIntCudaPointer
  → Int64CudaPointer                               — int64_t* GPU
    → GrowableInt64CudaPointer

CudaCore — CUDA Runtime API JNI 转发 (设备管理/内存/同步)
CudaJIT  — 运行时 CUDA 核函数 JIT 编译 (extends SimpleJIT.Engine)
CudaException — CUDA 操作异常
```
