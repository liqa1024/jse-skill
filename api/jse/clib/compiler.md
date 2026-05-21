# Compiler

> `jse.clib.Compiler`

**核心职能**：静态初始化时自动检测系统 C/C++ 编译器。Windows→MSVC（通过 `vswhere.exe` 定位 `cl.exe` + `VsDevCmd.bat`），Linux→gcc/g++ 优先，Mac→clang 回退。检测 GCC 版本（< 8.5 标记 `GCC_OLD` 并强制用户确认继续）。

```java
// === InitHelper ===
static class InitHelper {
    static boolean initialized()
    static void init()
}
static class Conf {
    static boolean FORCE                 // 是否强制编译器检测 (默认 true, 环境变量 JSE_FORCE_COMPILER)
}

// === 检测结果 ===
static final String TYPE                 // "msvc" / "gcc" / "clang" / "unknown"
static final String EXE_PATH             // 编译器可执行路径
static final String EXE_CMD              // 带引号拼接的执行命令
static final String MSVC_DEVCMD_PATH     // MSVC VsDevCmd.bat 路径 (仅 Windows)
static final boolean VALID               // 编译器是否可用
static final String GCC_VERSION          // GCC 版本号 (非 GCC 为 null)
static final boolean GCC_OLD             // GCC < 8.5
static final String C_COMPILER           // 传给 cmake 的 C 编译器标识
static final String CXX_COMPILER         // 传给 cmake 的 C++ 编译器标识

// --- 延迟打印 ---
static void printInfo()                  // 首次调用时输出编译器信息 + GCC 旧版警告+确认
```
