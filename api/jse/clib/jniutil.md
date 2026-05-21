# JNIUtil

> `jse.clib.JNIUtil`

**核心职能**：JNI 基础设施。提供 header-only 的 `jniutil.h` C 头文件自动安装、Java 数组类型检测(`jarrayType`)、JDK 厂商检查。**`LibBuilder` 为 `@ApiStatus.Internal`，不在此列**。`InitHelper.init()` 触发级联初始化：`Compiler` → `CMake` → `Ninja`。

```java
// === InitHelper ===
final static class InitHelper
static boolean initialized()             // JNIUtil 是否已初始化
static void init()                       // 手动强制初始化（级联 Compiler/CMake/Ninja）

// === 路径 ===
static final String HOME                 // JNI 库根目录 (结尾 '/')
static final String INCLUDE_DIR          // 头文件目录 (结尾 '/')
static final String HEADER_NAME = "jniutil.h"
static final String HEADER_PATH          // 头文件完整路径
static final String PKG_DIR              // 离线包下载缓存目录

// === Java 数组类型常量 ===
static final int JTYPE_NULL=0 / BYTE=1 / DOUBLE=2 / BOOLEAN=3 / CHAR=4 / SHORT=5 / INT=6 / LONG=7 / FLOAT=8
static int jarrayType(Object aJArray)    // 检测 Java 数组类型，返回上述常量之一
```
