# LmpCore

> `jse.clib.LmpCore`

**核心职能**：自动下载/编译 LAMMPS C++ 核心库。支持外部源码目录（`JSE_LMP_HOME`）或自动从 GitHub 下载指定 tag（默认 `stable_22Jul2025_update2`）。编译选项包括：动态库、异常支持、插件支持、自定义 PKG、MPI 可选。通过 `Dlfcn.dlopen()` 提升到 global（Linux 默认开启）。依赖 `MPICore`。

```java
static class InitHelper {
    static boolean initialized()
    static void init()
}
static class Conf {
    static String HOME                       // 外部 lammps 源码目录 (JSE_LMP_HOME)
    static String TAG                        // 下载 tag (JSE_LMP_TAG, 默认 stable_22Jul2025_update2)
    static int CMAKE_PARALLEL                // cmake 并行编译数 (JSE_LMP_CMAKE_PARALLEL, 默认 4)
    static boolean USE_MT                    // Windows /MT 静态链接开关 (默认 false)
    static final Map<String, String> CMAKE_SETTING        // 自定义 cmake 参数 (JSE_CMAKE_SETTING_LMP)
    static @Nullable String CMAKE_CXX_COMPILER            // JSE_CMAKE_CXX_COMPILER_LMP
    static @Nullable String CMAKE_CXX_FLAGS               // JSE_CMAKE_CXX_FLAGS_LMP
    static final Map<String, String> CMAKE_SETTING_SHARE  // 共享 cmake 参数 (JSE_CMAKE_SETTING_LMP_SHARE)
    static boolean DLOPEN                    // 是否 dlopen 提升到 global (默认 !IS_WINDOWS, JSE_LMP_DLOPEN)
}

// === 路径 ===
static final String ROOT                 // $JAR_DIR/lmp/
static final String INCLUDE_DIR          // lammps 头文件目录
static final String LIB_DIR              // lammps 动态库目录
static final String LIB_PATH             // lammps 动态库完整路径 (已 System.load)
static final String LLIB_PATH            // 链接库路径
static final String EXE_PATH             // lmp 可执行文件路径 (null=无)
static final String EXE_CMD              // lmp 执行命令
```
