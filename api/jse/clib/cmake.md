# CMake

> `jse.clib.CMake`

**核心职能**：自动检测并管理 CMake。优先检测系统 cmake（`Conf.USE_SYSTEM` 控制，默认 false），无则从 GitHub 下载预编译包并解压到 `$JAR_DIR/cmake/core/` 版本隔离目录。首次构建时输出信息。

```java
static class InitHelper {
    static boolean initialized()
    static void init()
}
static class Conf {
    static boolean USE_SYSTEM                // 是否使用系统 cmake (默认 false, 环境变量 JSE_USE_SYSTEM_CMAKE)
}

// === 常量 ===
static final String VERSION = "4.2.1"
static final String INTERNAL_HOME        // 内部 cmake 安装目录
static final String EXE_PATH             // cmake 可执行路径
static final String EXE_CMD              // 带引号拼接的执行命令

// --- 延迟打印 ---
static void printInfo()                  // 仅使用系统 cmake 时输出路径
```
