# SimpleJIT

> `jse.jit.SimpleJIT`

**核心职能**：`@ApiStatus.Experimental`。写入 C++ 源码至临时文件，调用系统编译器（cmake+ninja）编译为动态库并加载。`Engine` 为 `IJITEngine` 的核心实现，`Method` 为 `IJITMethod` 实现。

```java
static class InitHelper {
    static boolean initialized()
    static void init()
}
static class Conf {
    static final Map<String, String> CMAKE_SETTING     // JSE_CMAKE_SETTING_JIT
    static @Nullable String CMAKE_C_COMPILER / CMAKE_C_FLAGS
    static boolean CLEAN                               // 编译后是否清理临时目录 (默认 true, JSE_JIT_CLEAN)
}

// === 路径 ===
static final String LIB_DIR                         // JIT 引擎库目录 (版本隔离)
static final String CACHE_LIB_DIR                   // 缓存库目录
static final String LIB_PATH

// === 工厂 ===
static Engine engine()

// === Method (IJITMethod 实现) ===
static class Method implements IJITMethod
    @UnsafeJNI int invoke(IPointer aDataIn, IPointer rDataOut)  // → invokeMethod0 JNI

// === Engine (IJITEngine 实现) ===
static class Engine implements IJITEngine {
    // 构建器
    Engine setSrc(@Language("C++") String aSrc)             // 设置 C++ 代码（`extern "C"`内部）
    Engine setSrcCxx(@Language("C++") String aSrc)          // 设置额外的 C++ 代码 (`extern "C"`外部)
    Engine setProjectName(String)                           // 项目名 (影响缓存键)
    Engine setLibDir(String)                                // 库输出目录
    Engine setOptimLevel(int)                               // 优化等级
    Engine setMethodNames(String.../Collection)
    Engine addMethodName(CharSequence)
    Engine removeMethodName(CharSequence)
    Engine setCmakeSettings(Map<?,?>)                       // 自定义 cmake 参数
    Engine putCmakeSetting(CharSequence, CharSequence)
    Engine removeCmakeSetting(CharSequence)
    Engine setSrcDirIniter(IDirIniter)                      // 自定义源码目录初始化
    Engine setCmakeCxxCompiler(@Nullable String)
    Engine setCmakeCxxFlags(@Nullable String)

    // 查询
    boolean hasMethod(CharSequence)
    boolean isNull()                                        // 库是否无效
    String projectName()

    // 工作流
    void compile() throws Exception                         // 编译→加载动态库
    Method findMethod(CharSequence) throws JITException     // 查找方法
    void close() throws Exception                           // 释放库+清理
    boolean isClosed()

    // 可覆写钩子 (protected)
    void preInitCmakeCmd(List<String>)                      // cmake 命令前追加
    void postInitCmakeCmd(List<String>)                     // cmake 命令后追加
    String srcName() → "jitsrc.cpp"                        // 源码文件名
    String headName() → "jitsrc.h"                         // 头文件名
    void envChecker()                                       // 环境检测 (Compiler/CMake/Ninja)
}
```
