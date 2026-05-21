# Ninja

> `jse.clib.Ninja`

**核心职能**：自动检测并管理 Ninja 构建系统。逻辑与 CMake 镜像：优先系统 ninja（`Conf.USE_SYSTEM`，默认 false），无则从 GitHub 下载并解压。非 Windows 额外 `setExecutable`。

```java
static class InitHelper {
    static boolean initialized()
    static void init()
}
static class Conf {
    static boolean USE_SYSTEM                // 是否使用系统 ninja (默认 false, JSE_USE_SYSTEM_NINJA)
}

// === 常量 ===
static final String VERSION = "1.13.2"
static final String INTERNAL_HOME        // 内部 ninja 安装目录
static final String EXE_PATH
static final String EXE_CMD

// --- 延迟打印 ---
static void printInfo()                  // 仅系统 ninja 时输出路径
```
