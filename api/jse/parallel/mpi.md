# MPI

> `jse.parallel.MPI`

**核心职能**：`package-private` 构造的工具类。基于 `jse.clib.MPICore` JNI 实现，函数命名遵循 MPI C 标准。支持两种使用模式：(1) `import static MPI.Native.*` 传统 C 风格；(2) `MPI.init(args)` → `MPI.Comm.WORLD.rank()` → `MPI.close()` Java 风格。静态初始化时自动编译/加载 `mpijni` 动态库。

```java
// === 生命周期 ===
static void init(String[] aArgs) throws MPIException
static void init() throws MPIException
static boolean initialized() throws MPIException
static void close() throws MPIException
static boolean isClosed() throws MPIException

// === 线程安全初始化 ===
static int initThread(String[] aArgs, int aRequired) throws MPIException
static int initThread(int aRequired) throws MPIException

// === 工具 ===
static String libraryVersion() throws MPIException
static final int UNDEFINED

// === 附属内部类 ===
static class InitHelper {
    static boolean initialized()
    static void init()
}
static class Conf {
    static final Map<String, String> CMAKE_SETTING
    static @Nullable String CMAKE_C_COMPILER / CMAKE_CXX_COMPILER
    static @Nullable String CMAKE_C_FLAGS / CMAKE_CXX_FLAGS
    static boolean COPY_JARRAY          // 通讯前是否拷贝 Java 数组 (默认 true)
    static boolean USE_MIMALLOC         // 是否使用 MiMalloc 加速 (默认 Conf.USE_MIMALLOC)
}
static final class Thread {
    static final int SINGLE, FUNNELED, SERIALIZED, MULTIPLE
}
static final class Rank {
    static final int NULL, ANY, ROOT
}
static final class Tag {
    static final int ANY
}
```
