# JVM

> `jse.clib.JVM`

**核心职能**：自动探测 `$JAVA_HOME` 下的 JVM 动态库（`libjvm.so`/`jvm.dll`），依次搜索 `bin/server/` → `bin/client/` → `lib/server/` → `lib/client/`。Windows 上额外区分 LIB（运行时加载）和 LLIB（链接时使用 `.lib`）。

```java
static final String INCLUDE_DIR          // $JAVA_HOME/include/
static final String LIB_DIR              // JVM 动态库所在目录
static final String LIB_PATH             // JVM 动态库完整路径
static final String LLIB_DIR             // 链接库目录 (linux 同 LIB_DIR)
static final String LLIB_PATH            // 链接库路径 (linux 同 LIB_PATH)
```
