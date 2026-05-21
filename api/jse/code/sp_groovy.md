# SP.Groovy

> `jse.code.SP.Groovy`

**核心职能**：管理全局唯一的 GroovyShell，提供脚本执行、变量存取、类加载等能力。静态内部类，全局共享一个 GroovyShell，不实例化。

```java
// 获取 Groovy 运行时环境
static Binding context()              // 获取 Binding 上下文
static Binding binding()              // context() 的别名
static GroovyClassLoader classLoader()
static GroovyShell shell()

// 启动交互式 Shell（自动终端类型检测，预导入 jse 核心类）
static void runShell() throws Exception

// 执行 Groovy 代码（不返回值 / 返回值）
static void exec(String aText) throws Exception
static void execFile(String aFilePath) throws Exception
static Object eval(String aText) throws Exception
static Object evalFile(String aFilePath) throws Exception

// 运行文本脚本（支持传参）
static Object runText(String aText) throws Exception
static Object runText(String aText, String... aArgs) throws Exception

// 运行脚本文件
static Object run(String aScriptPath) throws Exception
static Object run(String aScriptPath, String... aArgs) throws Exception
static Object runScript(String aScriptPath) throws Exception
static Object runScript(String aScriptPath, String... aArgs) throws Exception

// 变量存取
static boolean hasValue(String aValueName) throws Exception
static Object getValue(String aValueName) throws Exception
static void setValue(String aValueName, Object aValue) throws Exception
static void removeValue(String aValueName) throws Exception
static Object get(String aValueName) throws Exception       // getValue 别名
static void set(String aValueName, Object aValue) throws Exception  // setValue 别名
static void remove(String aValueName) throws Exception      // removeValue 别名

// 调用方法（支持包名.类名.方法名 格式）
static Object invoke(String aMethodName) throws Exception
static Object invoke(String aMethodName, Object... aArgs) throws Exception

// 创建实例 / 加载类
static Object newInstance(String aClassName) throws Exception
static Object newInstance(String aClassName, Object... aArgs) throws Exception
static Class<?> getClass(String aClassName) throws Exception
static Class<?> parseClass(String aScriptPath) throws IOException
```
