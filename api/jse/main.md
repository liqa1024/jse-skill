# Main

> `jse.Main`

**核心职能**：解析命令行参数并路由到对应子系统（Groovy/Python Shell、LAMMPS、Jupyter Kernel、IDEA 项目初始化、JNI 管理、脚本执行）。静态工具类，通过 `java -jar jse.jar [options]` 运行，不直接实例化。

```java
// 获取 jse 的运行来源（如 "IDEA"、"JAR" 等），null 表示通过 class-path 运行
static @Nullable String RUN_FROM()

// 判断当前是否以 Jupyter Kernel 模式运行
static boolean IS_KERNEL()

// 注册一个全局自动关闭资源（替代 Runtime.addShutdownHook，线程安全且避免死锁）
static void addGlobalAutoCloseable(@Nullable AutoCloseable aAutoCloseable)

// 移除一个已注册的全局自动关闭资源
static void removeGlobalAutoCloseable(@Nullable AutoCloseable aAutoCloseable)

// 关闭所有已注册的全局自动关闭资源
static void closeAllAutoCloseable() throws Exception

// JVM 标准入口，委托给 main_ 执行参数路由
static void main(String[] aArgs)
```
