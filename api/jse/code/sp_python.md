# SP.Python

> `jse.code.SP.Python`

**核心职能**：通过 Jep 嵌入 CPython 解释器，提供与 Groovy 对等的 Python 脚本执行、变量存取能力，支持多线程 Jep 并行。静态内部类，全局共享一个 jep.Interpreter（主线程），支持 ThreadLocal 分支解释器。

```java
// ===== 初始化控制 =====
final static class InitHelper {
    static boolean initialized()
    static void init()
}

// ===== 版本与环境信息 =====
final static String JEP_VERSION       // "4.2.2"
final static String ASE_VERSION       // "3.25.0"
final static String PYTHON_PREFIX_DIR // 检测到的 Python 路径
final static boolean NUMPY_SUPPORT    // 是否支持 numpy
final static String JEP_LIB_DIR       // jep 二进制库目录
final static String JEP_LIB_PATH      // jep 二进制库路径

// ===== 编译配置 =====
final static class Conf {
    final static Map<String, String> CMAKE_SETTING    // 自定义 cmake -D 参数
    static @Nullable String CMAKE_C_COMPILER
    static @Nullable String CMAKE_C_FLAGS
    static boolean USE_MIMALLOC
}

// ===== 脚本执行 =====
static void exec(String aText) throws JepException
static void execFile(String aFilePath) throws JepException, IOException
static Object eval(String aText) throws JepException
static void runShell() throws JepException
static void runText(String aText) throws JepException
static void runText(String aText, String... aArgs) throws JepException
static void run(String aScriptPath) throws JepException, IOException
static void run(String aScriptPath, String... aArgs) throws JepException, IOException
static void runScript(String aScriptPath) throws JepException, IOException
static void runScript(String aScriptPath, String... aArgs) throws JepException, IOException

// ===== 变量存取 =====
static boolean hasValue(String aValueName) throws JepException
static Object getValue(String aValueName) throws JepException
static <T> T getValue(String aValueName, Class<T> aClazz) throws JepException
static void setValue(String aValueName, Object aValue) throws JepException
static void removeValue(String aValueName) throws JepException
static Object get(String aValueName) throws JepException       // getValue 别名
static void set(String aValueName, Object aValue) throws JepException  // setValue 别名
static void remove(String aValueName) throws JepException      // removeValue 别名
static <T> T getAs(Class<T> aExpectedType, String aValueName) throws JepException

// ===== 方法调用与实例化 =====
static Object invoke(String aMethodName) throws JepException
static Object invoke(String aMethodName, Map<String, Object> aKWArgs) throws JepException
static Object invoke(String aMethodName, Object... aArgs) throws JepException       // :note: 末尾为 Map 时自动作为 Python kwargs
static Object invoke(String aMethodName, Object[] aArgs, Map<String, Object> aKWArgs) throws JepException
static Object newInstance(String aClassName) throws JepException
static Object newInstance(String aClassName, Map<String, Object> aKWArgs) throws JepException
static Object newInstance(String aClassName, Object... aArgs) throws JepException    // :note: 末尾为 Map 时自动作为 Python kwargs
static Object newInstance(String aClassName, Object[] aArgs, Map<String, Object> aKWArgs) throws JepException
static PyObject getClass(String aClassName) throws JepException

// ===== 解释器生命周期 =====
static void close() throws JepException      // 关闭解释器
static boolean isClosed()                    // 是否已关闭
static void refresh() throws JepException    // 关闭后重新打开（清空所有变量）
static jep.Interpreter interpreter()         // 获取当前线程的解释器
static boolean isValidThread()               // 是否在主线程

// ===== 线程安全并行（自动为各线程创建独立 Jep 解释器） =====
static void parforWithInterpreter(int aSize, Closure<?> aGroovyTask)
static void parforWithInterpreter(int aSize, int aThreadNum, Closure<?> aGroovyTask)
static void parwhileWithInterpreter(ParforThreadPool.IParwhileChecker aChecker, Closure<?> aGroovyTask)
static void parwhileWithInterpreter(ParforThreadPool.IParwhileChecker aChecker, int aThreadNum, Closure<?> aGroovyTask)
static <U> Future<U> callAsyncWithInterpreter(Closure<U> aGroovyTask)
static <U> Future<U> supplyAsyncWithInterpreter(Closure<U> aGroovyTask)
static Future<Void> runAsyncWithInterpreter(Closure<?> aGroovyTask)

// ===== Python 包管理（基于 pip，半弃用） =====
// :note: 以下接口已半弃用，建议直接使用用户自己的 Python 包管理器（pip/conda 等）
static int downloadPackage(String aRequirement) throws IOException
static int downloadPackage(String aRequirement, boolean aIncludeDep) throws IOException
static int downloadPackage(String aRequirement, boolean aIncludeDep, String aPlatform) throws IOException
static int downloadPackage(String aRequirement, boolean aIncludeDep, String aPlatform, String aPythonVersion) throws IOException
static int downloadPackage(String aRequirement, boolean aIncludeDep, String aPlatform, String aPythonVersion, String aIndexUrl) throws IOException
static int downloadPackage(String aRequirement, String aPlatform) throws IOException
static int downloadPackage(String aRequirement, String aPlatform, String aPythonVersion) throws IOException
static int downloadPackage(String aRequirement, String aPlatform, String aPythonVersion, String aIndexUrl) throws IOException
static int installPackage(String aRequirement) throws IOException
static int installPackage(String aRequirement, boolean aIncludeDep) throws IOException
static int installPackage(String aRequirement, boolean aIncludeDep, boolean aIncludeIndex) throws IOException
static void installAse() throws IOException   // 下载并安装指定版本的 ASE
```
