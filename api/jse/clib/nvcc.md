# NVCC

> `jse.clib.NVCC`

**核心职能**：检测系统的 `nvcc` 编译器及 CUDA 可用性。仅检测不编译——区别于 `jse.gpu.CudaCore`。`printInfo()` 提供安装指引。

```java
static class InitHelper {
    static boolean initialized()
    static void init()
}

// === 检测结果 ===
static final String EXE_PATH              // nvcc 可执行路径
static final String EXE_CMD
static final boolean VALID                // 是否有可用 CUDA

// --- 延迟打印 ---
static void printInfo()                   // 首次调用时输出 CUDA 检测结果 + 下载链接
```
