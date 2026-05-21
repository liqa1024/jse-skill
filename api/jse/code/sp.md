# SP

> `jse.code.SP`

**核心职能**：统一管理 Groovy 和 Python 两种脚本语言的执行环境，并内置 Jupyter Kernel 支持。静态工具类，不实例化。

```java
// ===== 路径常量 =====
// 脚本路径查找优先级：1. 工作目录（IO.toAbsolutePath） 2. 以下历史遗留目录（不推荐新代码依赖）
final static String GROOVY_SP_DIR    // "script/groovy/"（Groovy 脚本回退目录）
final static String PYTHON_SP_DIR    // "script/python/"（Python 脚本回退目录）
final static String GROOVY_LIB_DIR   // 外部 Groovy 库目录
final static String JAR_LIB_DIR      // 外部 jar 库目录
final static String PYTHON_PKG_DIR   // Python 离线包目录 (.pypkg/)
final static String PYTHON_LIB_DIR   // 外部 Python 库目录（仅 jse 使用）

// ===== 自动检测并运行脚本 =====
// 后缀规则：.groovy → Groovy，.py/.jsepy → Python，其他 → 优先 Groovy（先试 .groovy 再试 .py）
static void run(String aScriptPath) throws Exception
static void run(String aScriptPath, String... aArgs) throws Exception
static void runScript(String aScriptPath) throws Exception
static void runScript(String aScriptPath, String... aArgs) throws Exception
```
