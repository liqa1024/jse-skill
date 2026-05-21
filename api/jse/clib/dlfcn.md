# Dlfcn

> `jse.clib.Dlfcn`

**核心职能**：通过 JNI 调用 C 的 `dlopen()` 将动态库提升到 global 作用域，解决部分 lammps 插件找不到 lammps 库的链接问题。采用 jep 同款实现——仅 `dlopen` 不涉及其他 `dlfcn.h` 接口。非 Unix 系统不做任何操作。

```java
static class InitHelper {
    static boolean initialized()
    static void init()
}
static class Conf {
    static final Map<String, String> CMAKE_SETTING    // 自定义 cmake 参数 (JSE_CMAKE_SETTING_DLFCN)
    static @Nullable String CMAKE_C_COMPILER           // 自定义 C 编译器 (JSE_CMAKE_C_COMPILER_DLFCN)
    static @Nullable String CMAKE_C_FLAGS              // 自定义 C 编译选项 (JSE_CMAKE_C_FLAGS_DLFCN)
}

// === 路径 ===
static final String LIB_DIR                        // dlfcn JNI 库目录 (版本隔离)
static final String LIB_PATH                       // dlfcn JNI 库完整路径

// === JNI native ===
native static void dlopen(String aPath)            // 调用 dlopen() 提升库到 global
```
