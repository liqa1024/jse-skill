# MPICore

> `jse.clib.MPICore`

**核心职能**：检测系统的 `mpiexec` 可执行文件及其可用性。仅检测不编译——区别于 `jse.parallel.MPI`。`printInfo()` 在无 MPI 时给出安装指引。

```java
static class InitHelper {
    static boolean initialized()
    static void init()
}

// === 检测结果 ===
static final String EXE_PATH              // mpiexec 可执行路径 (null=未检测到)
static final String EXE_CMD               // 带引号拼接的执行命令
static final boolean VALID                // 是否有可用 MPI

// --- 延迟打印 ---
static void printInfo()                   // 首次调用时输出 MPI 检测结果 + 安装指引
```
