# MiMalloc

> `jse.clib.MiMalloc`

**核心职能**：集成 Microsoft mimalloc 高性能内存分配器，加速 C 层 `malloc`/`free`。从内部资源 zip 解压源码并通过 cmake 编译为动态库。旧版 GCC（< 8.5）直接禁用。

```java
static class InitHelper {
    static boolean initialized()
    static void init()
}
static class Conf {
    static final Map<String, String> CMAKE_SETTING     // 自定义 cmake 参数 (JSE_CMAKE_SETTING_MIMALLOC)
    static @Nullable String CMAKE_C_COMPILER            // JSE_CMAKE_C_COMPILER_MIMALLOC
    static @Nullable String CMAKE_CXX_COMPILER          // JSE_CMAKE_CXX_COMPILER_MIMALLOC
    static @Nullable String CMAKE_C_FLAGS               // JSE_CMAKE_C_FLAGS_MIMALLOC
    static @Nullable String CMAKE_CXX_FLAGS             // JSE_CMAKE_CXX_FLAGS_MIMALLOC
}

// === 常量 ===
static final String VERSION = "2.2.4"
static final String HOME                            // 版本隔离安装目录
static final String LIB_DIR                         // 动态库目录
static final String INCLUDE_DIR                     // 头文件目录 (含 mimalloc.h)
static final @NotNull String LIB_PATH
static final @NotNull String LLIB_PATH
```
