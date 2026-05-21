# OS

> `jse.code.OS`

**核心职能**：提供操作系统级别的基础设施——系统类型判定、环境变量读取、工作目录获取、系统命令执行，以及 SLURM 集群资源管理。静态工具类，不实例化。

```java
// ===== 初始化控制 =====
final static class InitHelper {
    static boolean initialized()  // 静态常量是否已初始化
    static void init()            // 手动触发初始化
}

// ===== 平台标识 =====
final static String OS_NAME       // System.getProperty("os.name")
final static boolean IS_WINDOWS   // 是否 Windows
final static boolean IS_MAC       // 是否 macOS
final static String NO_LOG_LINUX  // "/dev/null"
final static String NO_LOG_WIN    // "NUL"
final static String NO_LOG        // Win: "NUL", Unix: "/dev/null"

// ===== 路径常量 =====
// 所有目录常量均为绝对路径，以 `/` 结尾，可直接拼接文件名
final static String JAVA_HOME         // JDK 路径
final static String JAVA_HOME_DIR     // JDK 路径（内部合法化，可拼接）
final static String USER_HOME         // 用户目录
final static String USER_HOME_DIR     // 用户目录（内部合法化，可拼接）
final static String WORKING_DIR       // jse 工作目录（内部合法化，可拼接）
final static String JAR_PATH          // jse 核心 jar 文件路径
final static String JAR_DIR           // jse 核心 jar 所在文件夹（内部合法化，可拼接）
final static String JAR_DIR_FILESYSTEM // jar 目录文件系统类型
final static boolean JAR_DIR_BAD_FILESYSTEM // 是否过时文件系统（Lustre/PanFS/GPFS）

// ===== 全局系统命令执行器 =====
final static ISystemExecutor EXEC                         // Win: PWSH(USE_PWSH) / PowerShell; 其他: Bash
                                                          // 自动注册 Main.addGlobalAutoCloseable

// ===== 环境变量读取 =====
static @Nullable String env(String aName)                         // 获取环境变量，失败返回 null
static String env(String aName, String aDefault)                  // 获取环境变量，失败返回默认值
static String @NotNull[] envPath(String aName)                    // 获取路径数组（按 File.pathSeparator 分隔）
static String[] envPath(String aName, String[] aDefault)
static @NotNull Map<String, String> envMap(String aName)          // 获取 Map（格式 k1:v1,k2:v2,...）
static Map<String, String> envMap(String aName, Map<String, String> aDefault)
static int envI(String aName, int aDefault)                       // 获取 int 环境变量
static double envD(String aName, double aDefault)                 // 获取 double 环境变量
static boolean envZ(String aName, boolean aDefault)               // true: "true/t/on/yes/1"

// ===== 系统命令执行（委托给 EXEC） =====
// :note: 以下均为 @VisibleForTesting 接口，Groovy 脚本优先使用
@VisibleForTesting static int system(String aCommand)             // → EXEC.system, 同步执行
@VisibleForTesting static int system(String aCommand, String aOutFilePath) // → EXEC.system, 重定向输出
@VisibleForTesting static Future<Integer> submitSystem(String aCommand)    // → EXEC.submitSystem, 异步提交
@VisibleForTesting static Future<Integer> submitSystem(String aCommand, String aOutFilePath)
@VisibleForTesting static List<String> system_str(String aCommand)         // → EXEC.system_str, 同步获取输出
@VisibleForTesting static Future<List<String>> submitSystem_str(String aCommand) // → EXEC.submitSystem_str, 异步获取输出

// 对过时文件系统发出警告（仅首次调用时打印）
static void printFilesystemInfo() throws Exception
```
