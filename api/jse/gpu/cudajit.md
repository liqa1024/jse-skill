# CudaJIT

> `jse.gpu.CudaJIT`

**核心职能**：`@ApiStatus.Experimental`。`extends SimpleJIT.Engine`，将 `.cu` 源码编译为动态库并加载。覆写 `writeCmakeFile`（`@ApiStatus.Internal`）生成完整的 CUDA CMakeLists.txt。支持三个优化级别：`JSE_OPTIM_MAX`（native arch + FMA + fast math）、`JSE_OPTIM_BASE`（默认，native arch + fast math）、`JSE_OPTIM_COMPAT`（仅 fast math，无 native arch）。

```java
static Engine engine()                               // 创建编译引擎

static class Engine extends SimpleJIT.Engine {
    Engine setCmakeCudaCompiler(@Nullable String)    // 自定义 CUDA 编译器
    Engine setCmakeCudaFlags(@Nullable String)       // 自定义 CUDA 编译选项
    // 覆写: srcName()→"jitsrc.cu"
    // 覆写: envChecker()→NVCC.printInfo()
    // 覆写: writeCmakeFile (CUDA+CXX, 三级优化选项)
}
```
