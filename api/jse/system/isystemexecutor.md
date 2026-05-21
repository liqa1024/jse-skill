# ISystemExecutor

> `jse.system.ISystemExecutor`

**核心职能**：`extends IThreadPool implements AutoCloseable`。统一系统命令执行接口。线程安全（同一实例可并行调用）。支持同步/异步执行、输出重定向、文件传输。**`validPath`/`makeDir`/`delete`/`isFile`/`isDir`/`list` 是 `jse.IO` 同名方法的镜像**——本地执行器直接委托 `IO` 静态方法，远程执行器通过 SFTP 协议在远程服务器上执行等效操作。

**资源管理**：继承 `IThreadPool` 的 `close()`（→ `shutdown()` + `awaitTermination()`）和 `shutdown()`（内部接口）。jse 通过 `ReferenceChecker` 实现 GC 自动释放——对象被 GC 时自动调用 `close()`，Groovy 脚本无需手动释放。

```java
// --- 文件系统操作 (jse.IO 镜像, 本地=IO.xxx(), 远程=SFTP) ---
void validPath(String aPath) throws Exception        // 合法化路径（创建父目录）
void makeDir(String aDir) throws Exception            // 创建目录
void removeDir(String aDir) throws Exception           // @ApiStatus.Internal
void delete(String aPath) throws Exception
boolean isFile(String aFilePath) throws Exception
boolean isDir(String aDir) throws Exception
String @NotNull[] list(String aDir) throws Exception

// --- 文件传输 (本地=空操作, 远程=SFTP上传/下载) ---
void putFiles(Iterable<? extends CharSequence> aFiles) throws Exception
void getFiles(Iterable<? extends CharSequence> aFiles) throws Exception
void putFiles(String... aFiles) throws Exception
void getFiles(String... aFiles) throws Exception

// --- 配置 ---
ISystemExecutor setWorkingDir(@Nullable String aWorkingDir) throws Exception
ISystemExecutor setNoSTDOutput() / setNoSTDOutput(boolean)
boolean noSTDOutput()
ISystemExecutor setNoERROutput() / setNoERROutput(boolean)
boolean noERROutput()

// --- 同步执行 ---
int system(String aCommand)                          // 执行命令，返回退出码
int system(String aCommand, String aOutFilePath)     // 输出→文件
int system_str(String aCommand, List<String> rOutLines)  // 输出行→List
List<String> system_str(String aCommand)             // 返回输出行列表

// --- 异步执行 ---
Future<Integer> submitSystem(String aCommand)
Future<Integer> submitSystem(String aCommand, String aOutFilePath)
Future<Integer> submitSystem_str(String aCommand, List<String> rOutLines)
Future<List<String>> submitSystem_str(String aCommand)

// --- Groovy (@VisibleForTesting) ---
default void mkdir(String aDir) throws Exception          // → makeDir
default void rmdir(String aDir) throws Exception          // → removeDir, @ApiStatus.Internal
```
