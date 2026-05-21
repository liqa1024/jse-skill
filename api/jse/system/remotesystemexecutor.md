# RemoteSystemExecutor

> `jse.system.RemoteSystemExecutor`

**核心职能**：`extends AbstractSystemExecutor`。远程执行器的抽象基类。与 `LocalSystemExecutor` 的核心区别：
- **文件系统操作**（`validPath`/`makeDir`/`delete`/`isFile`/`isDir`/`list`）不再委托本地 `IO`，而需通过远程协议（如 SSH SFTP）在远端服务器上执行
- **`putFiles`/`getFiles`** 不再是空操作，需实际跨网络传输文件（上传/下载）
- **`setWorkingDir`** 通常需要同时管理本地和远端两套工作目录

当前唯一子类为 `SSHSystemExecutor`（JSch SFTP 实现）。
