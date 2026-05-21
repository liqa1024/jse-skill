# SSHSystemExecutor

> `jse.system.SSHSystemExecutor`

**核心职能**：`extends RemoteSystemExecutor implements ISavable`。通过 JSch 库 SSH 连接到远程服务器执行命令。与本地执行器的关键差异：
- **文件系统**：`validPath`/`makeDir`/`delete`/`isFile`/`isDir`/`list` 通过 SFTP 协议在远程服务器执行（而非本地 `IO` 镜像），每个操作自动打开/关闭 `ChannelSftp`
- **文件传输**：`putFiles`/`getFiles` 实际跨网络 SFTP 上传/下载，参数使用相对路径（统一 `/` 分隔）基于 `localWorkingDir`/`remoteWorkingDir`。路径在两端共享，不能拼接含盘符的绝对路径
- **工作目录**：分离 `localWorkingDir` 和 `remoteWorkingDir`，所有远程命令前自动加 `cd remoteWorkingDir`
- **取消机制**：`SSHSystemFuture` 通过 `ChannelExec.sendSignal("2")` 发送 SIGINT 而非 `Process.destroy()`

内部 `SSHCore`（package-private）封装 JSch Session 管理和 SFTP 传输。构造失败自动 `close()`。

```java
// === Map 构造 ===
// 区分大小写，按以下顺序依次尝试匹配到第一个存在的 key：
//   Hostname / hostname / host / h              — 远程服务器地址（必填）
//   Username / username / user / u              — SSH 用户名（必填）
//   Password / password / pw                    — 密码认证（与 KeyPath 二选一）
//   KeyPath / keypath / key / k                 — 私钥路径（默认 ~/.ssh/id_rsa，与 Password 二选一）
//   Port / port / p                             — SSH 端口（默认 22）
//   LocalWorkingDir / localworkingdir / lwd      — 本地工作目录
//   RemoteWorkingDir / remoteworkingdir / rwd / wd  — 远端工作目录
//   CompressLevel / compresslevel / cl           — SSH 压缩等级（默认 -1 禁用，>0 启用 zlib）
//   BeforeCommand / beforecommand / bcommand / bc  — 每条命令前额外执行的前置命令
//   IOThreadNumber / iothreadnumber / IOThreadNum / iothreadnum / ion  — @Deprecated SFTP 并行线程数（高度弃用，默认 -1 不并行）
SSHSystemExecutor(Map<?,?> aArgs) throws Exception

// === 运行时配置 ===
SSHSystemExecutor setLocalWorkingDir(String) / setRemoteWorkingDir(String)
SSHSystemExecutor setCompressLevel(int) throws Exception
SSHSystemExecutor setBeforeCommand(String)     // 每条命令前自动执行的前置命令

// === ISavable (@ApiStatus.Internal) ===
@ApiStatus.Internal void save(Map rSaveTo)     // 保存连接参数

// === Builder (@ApiStatus.Internal) ===
@ApiStatus.Internal static Builder builder()
@ApiStatus.Internal static final class Builder {
    @Deprecated Builder setNthreadsIO(int)  // 高度弃用
    Builder setUsername(String) / setHostname(String) / setPort(int)
    Builder setLocalWorkingDir(String) / setRemoteWorkingDir(String)
    Builder setPassword(String) / setKeyPath(String)
    Builder setCompressLevel(int)
    Builder setBeforeCommand(String)
    SSHSystemExecutor build() throws Exception
}
```
