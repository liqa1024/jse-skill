# CudaCore

> `jse.gpu.CudaCore`

**核心职能**：`@ApiStatus.Experimental`。封装 CUDA Runtime API 的核心 JNI 库（cudacore）。编译时依赖 `NVCC`（无 CUDA 直接抛异常）。静态初始化时自动注册 `cudaDeviceSynchronize` 为全局 `AutoCloseable`，确保 JVM 关闭时同步设备。

```java
static class InitHelper {
    static boolean initialized()
    static void init()
}
static class Conf {
    static final Map<String, String> CMAKE_SETTING     // JSE_CMAKE_SETTING_CUDA
    static @Nullable String CMAKE_CXX_COMPILER / CMAKE_CXX_FLAGS
    static boolean USE_MIMALLOC                         // JSE_USE_MIMALLOC_CUDA
}

// === 路径 ===
static final String LIB_DIR / LIB_PATH

// === 设备管理 ===
static native void cudaDeviceSynchronize() throws CudaException
static native void cudaExceptionCheck(int aCudaErrorCode) throws CudaException
static native int cudaGetDeviceCount() throws CudaException
static native void cudaSetDevice(int aDevice) throws CudaException
static native int cudaGetDevice() throws CudaException

// === 内存管理 (包级私有，由 CudaPointer 及其子类调用) ===
static long cudaMalloc(long aCount) throws CudaException
static native void cudaFree(long aPtr) throws CudaException

// === 数据传输 (D=Device显存, H=Host主机内存) ===
static native void cudaMemcpyH2D(long aSrc, long rDest, long aCount) throws CudaException
static native void cudaMemcpyD2H(long aSrc, long rDest, long aCount) throws CudaException
static native void cudaMemcpyD2D(long aSrc, long rDest, long aCount) throws CudaException

// === 显存设置 ===
static native void cudaMemset(long aPtr, int aValue, long aCount) throws CudaException
```
