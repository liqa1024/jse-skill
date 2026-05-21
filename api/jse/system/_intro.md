# `jse.system`

> 系统命令执行器——统一接口在多环境执行系统命令。本地通过 `ProcessBuilder` 运行（支持 bash/cmd/PowerShell/pwsh/wsl/srun/python/jse），远程通过 SSH（JSch）执行。`ISystemExecutor` 继承 `IThreadPool`（实现 `AutoCloseable`），支持同步/异步提交、输出重定向、文件上传下载，通过 `ReferenceChecker` 实现 GC 自动释放。`@VisibleForTesting` 别名提供 Groovy 简洁构造。

## 架构总览 (Architecture)

```
ISystemExecutor (extends IThreadPool)
  → AbstractSystemExecutor — 同步/异步包装, 输出流管理, shutdown 生命周期
    → LocalSystemExecutor — ProcessBuilder 本地执行, LocalSystemFuture
      → JSESystemExecutor — java -jar JSE (-t / -pythontext)
        → JSE (@VisibleForTesting, final)
      → BashSystemExecutor — bash -c
        → Bash (@VisibleForTesting, final)
      → CMDSystemExecutor — cmd /c, GBK charset
        → CMD (@VisibleForTesting, final)
      → PowerShellSystemExecutor — PowerShell -EncodedCommand, Base64(UTF-16LE)
        → PowerShell (@VisibleForTesting, final)
      → PWSHSystemExecutor — pwsh -of Text -ec, Base64(UTF-16LE)
        → PWSH (@VisibleForTesting, final)
      → WSLSystemExecutor — wsl bash -c
        → WSL (@VisibleForTesting, final)
      → PythonSystemExecutor — python/python3 -c
        → Python (@VisibleForTesting, final)
      → SRUNSystemExecutor — SLURM srun job steps, 资源分配/归还
        → SRUN (@VisibleForTesting, final)
    → RemoteSystemExecutor (抽象) — 远程执行标记
      → SSHSystemExecutor + ISavable — JSch SSH, Builder/Map构造, 并行IO传输
        → SSH (@VisibleForTesting, final)
```
