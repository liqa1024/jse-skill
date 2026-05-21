# SSHCore

> `jse.system.SSHCore`

> 此类为 @ApiStatus.Internal / package-private

**核心职能**：`final class implements AutoCloseable`。封装 JSch Session 管理和 SFTP 传输，供 `SSHSystemExecutor` 内部使用。创建时自动连接服务器，自动跳过首次登录的 "yes/no" 询问。通过 `setPassword` / `setKey` 切换认证方式。

```java
// === 构造/工厂 ===
static SSHCore of(String aUsername, String aHostname, int aPort,
                  @Nullable String aLocalWorkingDir, @Nullable String aRemoteWorkingDir,
                  @Nullable String aPassword, @Nullable String aKeyPath,
                  int aCompressLevel, @Nullable String aBeforeCommand) throws Exception
static SSHCore load(Map aJson) throws Exception

// === 运行时配置（fluent）===
SSHCore setLocalWorkingDir(@Nullable String)
SSHCore setRemoteWorkingDir(@Nullable String)
SSHCore setCompressLevel(int) throws Exception
SSHCore setBeforeCommand(String)
SSHCore setPassword(String) throws Exception
SSHCore setKey(String) throws Exception

// === 连接管理 ===
boolean isConnecting()
synchronized void connect() throws JSchException
void disconnect()
void close()
synchronized Session session()

// === 命令执行 ===
ChannelExec systemChannel(String aCommand, boolean aNoERROutput) throws Exception

// === 远程文件系统（SFTP）===
void removeDir(String) throws Exception
void makeDir(String) throws Exception
boolean isDir(String) throws Exception
boolean isFile(String) throws Exception
void delete(String) throws Exception
void validPath(String) throws Exception
String[] list(String) throws Exception

// === 单线程文件传输 ===
void putFiles(Iterable<String>) throws Exception
void getFiles(Iterable<String>) throws Exception

// === 并发文件传输 ===
void putFiles(Iterable<String>, int aThreadNumber) throws Exception
void getFiles(Iterable<String>, int aThreadNumber) throws Exception

// === 持久化 ===
void save(Map rSaveTo)
```
