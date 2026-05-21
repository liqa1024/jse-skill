# Conf

> `jse.code.Conf`

**核心职能**：集中管理 jse 所有可配置的全局行为开关。每个 `Conf.XYZ` 对应环境变量 `JSE_XYZ`（启动前设置），也可在 Groovy 脚本中直接修改（运行时生效，外部库路径类例外）。静态常量类，不实例化。

```java
// ===== 调试与兼容性 =====
static boolean DEBUG                   // 开启 debug 模式（含 jse 内核栈信息）。默认 false，环境变量 JSE_DEBUG
static boolean JDK_CHECK               // JDK 版本检测与兼容性警告。默认 true，环境变量 JDK_CHECK
static boolean OPERATION_CHECK         // 运算边界检测（jse 2.7.7 之前不检测）。默认 true，环境变量 JSE_OPERATION_CHECK
static boolean ENV_PROXY               // 优先采用环境变量 HTTP/HTTPS 代理。默认 true，环境变量 JSE_ENV_PROXY
static boolean STRICT_IO               // IO 严格模式，格式错误时抛异常而非返回 null。默认 true，环境变量 JSE_STRICT_IO
static boolean NATIVE_OPERATION        // native 优化加速（需要编译器，不再符合 IEEE 标准）。默认 false，环境变量 JSE_NATIVE_OPERATION
static boolean JEP_ADD_GROOVY_HOOK     // 将 Groovy 脚本库加入 jep import hook。默认 false，环境变量 JSE_JEP_ADD_GROOVY_HOOK
static boolean INCLUDE_WORKING_DIR     // 将工作目录包含到类搜索路径。默认 true，环境变量 JSE_INCLUDE_WORKING_DIR
static boolean USE_PWSH                // Windows 上使用新版 PowerShell (pwsh)。默认 false，环境变量 JSE_USE_PWSH

// ===== Kernel 模式 =====
static boolean KERNEL_THREAD_INTERRUPT // Jupyter 模式下开启 ThreadInterrupt。默认 true，环境变量 JSE_KERNEL_THREAD_INTERRUPT
static boolean KERNEL_SHOW_FIGURE      // Jupyter 模式下弹出窗口 vs 内联渲染。默认 false，环境变量 JSE_KERNEL_SHOW_FIGURE

// ===== 目录与路径 =====
static String TEMP_WORKING_DIR         // 临时工作目录模板，%n 为子目录占位符。默认 ".temp/%n/"，环境变量 JSE_TEMP_WORKING_DIR
static String WORKING_DIR_OF(String aUniqueName)                // 获取临时工作目录路径（绝对路径，不创建）
static String WORKING_DIR_OF(String aUniqueName, boolean aRelative) // 同上，aRelative=true 返回相对路径

// ===== 输出与终端 =====
static boolean UNICODE_SUPPORT         // System.out/err 是否支持 Unicode 字符。默认 true，环境变量 JSE_UNICODE_SUPPORT
static boolean PBAR_ERR_STREAM         // 进度条输出到 System.err。默认 true，环境变量 JSE_PBAR_ERR_STREAM

// ===== 并行计算 =====
static boolean PARFOR_NO_COMPETITIVE   // parfor 禁用竞争模式（保证可重复性）。默认 false，环境变量 JSE_PARFOR_NO_COMPETITIVE
static int PARFOR_THREAD_NUMBER        // parfor 默认线程数。默认 availableProcessors()，环境变量 JSE_PARFOR_THREAD_NUMBER

// ===== 外部库路径（脚本中修改无效，需通过环境变量在启动前设置） =====
static String @NotNull[] GROOVY_EXLIB_DIRS   // 外置 Groovy 库路径数组。环境变量 JSE_GROOVY_EXLIB_DIRS
static String @NotNull[] JAR_EXLIB_DIRS      // 外置 Jar 库路径数组。环境变量 JSE_JAR_EXLIB_DIRS
static String @NotNull[] PYTHON_EXLIB_DIRS   // 外置 Python 库路径数组。环境变量 JSE_PYTHON_EXLIB_DIRS

// ===== 缓存与编译 =====
static boolean NO_CACHE                // 关闭数组缓存（降低老版本 JDK 内存泄漏风险）。默认 false，环境变量 JSE_NO_CACHE
static int VERSION_MASK                // 用户自定义版本掩码，区分不同环境的 JNI 依赖。默认 0，环境变量 JSE_VERSION_MASK
static boolean USE_MIMALLOC            // 使用 MiMalloc 加速 C 内存分配。默认 true，环境变量 JSE_USE_MIMALLOC
static @Nullable String CMAKE_C_COMPILER    // 全局 cmake C 编译器。环境变量 JSE_CMAKE_C_COMPILER
static @Nullable String CMAKE_CXX_COMPILER  // 全局 cmake C++ 编译器。环境变量 JSE_CMAKE_CXX_COMPILER
static @Nullable String CMAKE_C_FLAGS       // 全局 cmake C 编译参数。环境变量 JSE_CMAKE_C_FLAGS
static @Nullable String CMAKE_CXX_FLAGS     // 全局 cmake C++ 编译参数。环境变量 JSE_CMAKE_CXX_FLAGS
static String LIB_EXTENSION            // 动态库后缀（Win: .dll, Mac: .dylib, Linux: .so）
static String LLIB_EXTENSION           // 链接库后缀（Win: .lib, Mac: .dylib, Linux: .so）

// 在指定目录查找匹配项目名的库文件，未找到返回 null
static @Nullable String LIB_NAME_IN(String aLibDir, String aProjectName)
static @Nullable String LLIB_NAME_IN(String aLibDir, String aProjectName)
```
