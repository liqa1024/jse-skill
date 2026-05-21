# jse — 系统命令基础

jse 通过统一的 `ISystemExecutor` 接口执行系统命令。一次性命令走 `OS.system`/`OS.system_str` 快捷方法（委托给全局执行器 `OS.EXEC`）；需要工作目录、输出重定向、异步等精细控制时显式创建执行器；执行 jse/Python 子脚本用 `JSE`/`Python` 执行器。远程和 SLURM 见 `system2.md`。

> **类引用**：`OS`=`jse.code.OS`，`Bash`=`jse.system.Bash`，`CMD`=`jse.system.CMD`，`PowerShell`=`jse.system.PowerShell`，`PWSH`=`jse.system.PWSH`，`WSL`=`jse.system.WSL`，`JSE`=`jse.system.JSE`，`JSESystemExecutor`=`jse.system.JSESystemExecutor`，`Python`=`jse.system.Python`，`PythonSystemExecutor`=`jse.system.PythonSystemExecutor`
>
> `OS.system`/`OS.system_str`/`OS.submitSystem`/`OS.submitSystem_str` 为 `@VisibleForTesting` 别名，委托给 `OS.EXEC`。Groovy 脚本中优先使用；需要精细控制时手动创建新的基本执行器。

## OS 快捷方式

最简单的命令执行方式，委托给 `OS.EXEC`（Linux 上为 `Bash`，Windows 上为 `PowerShell` 或 `PWSH`），适合一次性命令。

```groovy
// 同步 — 返回退出码
int ret = OS.system("echo hello")
OS.system("echo hello", "output.txt")             // 输出重定向到文件
List<String> lines = OS.system_str("echo hello")  // 获取命令输出按行

// 异步 — 返回 Future
Future<Integer> fut = OS.submitSystem("sleep 2 && echo done")
List<String> lines = OS.submitSystem_str("echo hello").get()
```

## 基本执行器

所有本地执行器实现了 `ISystemExecutor`，通过 `ProcessBuilder` 启动进程，自动读取转发 stdout/stderr 防止死锁。

| 执行器 | 命令前缀 | 适用场景 |
|---|---|---|
| `Bash` | `bash -c` | Linux / macOS / WSL |
| `CMD` | `cmd /c` | Windows 命令提示符，GBK 编码 |
| `PowerShell` | `PowerShell -EncodedCommand` | Windows PowerShell 5，Base64(UTF-16LE) 传参 |
| `PWSH` | `pwsh -of Text -ec` | PowerShell 7+ 跨平台版 |
| `WSL` | `wsl bash -c` | Windows Subsystem for Linux |

> `PowerShell`/`PWSH` 将命令经 Base64 编码后通过 `-EncodedCommand` 传入，避免转义问题。

```groovy
// Bash
Bash bash = new Bash()
bash.system("gcc -O3 code.c -o code")

// Windows CMD
CMD cmd = new CMD()
cmd.system("dir /B")

// PowerShell
PowerShell ps = new PowerShell()
ps.system("Get-ChildItem | Select-Object Name")
```

### 平台检测与选择

可以通过 `OS.IS_WINDOWS` 选择执行器来实现跨平台脚本。例如 Windows 上使用 `PWSH` 或 `PowerShell`，其余情况使用 `Bash`；或在某些情况在 Windows 上使用 `WSL` 来保证行为完全一致：

```groovy
// 两者都兼容的命令（OS.EXEC 一致行为）
ISystemExecutor exec = OS.IS_WINDOWS ? new PWSH() : new Bash()
exec.system("echo hello")

// 调用 WSL 保证行为完全一致
WSL wsl = new WSL()
wsl.system("grep pattern file.txt")
```

## 执行 jse / Python 子脚本

> ⚠️ `Python` 和 `JSESystemExecutor(Python 模式)` 依赖 JEP（Java Embedded Python），首次使用前需运行 `jse --jnibuild`。未构建时直接调用会触发交互式自动构建导致卡死。
>
> **TODO(jse)**：目前无 API 可在不触发初始化的前提下检测 JNI 是否已构建。

```groovy
// 在子进程中执行 Groovy 文本（等价于 jse -t）
JSE jseExec = new JSE()
jseExec.system("println(CS.VERSION)")

// 在子进程中执行 Python 文本（等价于 jse --pythontext）
JSESystemExecutor jsePy = new JSESystemExecutor(true)
jsePy.system("import jse; print(jse.code.CS.VERSION)")

// 执行 Python 代码
Python py = new Python()               // python -c
PythonSystemExecutor py3 = new PythonSystemExecutor(true)  // python3 -c
py.system("print('hello')")
```

## ISystemExecutor — 显式控制

显式创建执行器可配置工作目录、抑制输出、文件操作等。

### 基本配置

```groovy
ISystemExecutor exec = new Bash()
exec.setWorkingDir("/path/to/work")
exec.setNoSTDOutput(true)          // 禁止 stdout 打印到控制台
exec.setNoERROutput(false)         // 保留 stderr

int ret = exec.system("make")
```

### 资源释放

`ISystemExecutor` 实现 `AutoCloseable`，jse 通过 `ReferenceChecker` 在对象被 GC 时自动释放。Groovy 脚本中**无需手动释放**。

### 文件系统操作

执行器提供与 `IO` 镜像的文件方法：本地执行器委托 `IO` 静态方法（详见 `io.md`），远程执行器通过 SFTP。

```groovy
exec.validPath("/path/to/output.txt")  // 确保父目录存在
exec.makeDir("/path/to/newdir")
exec.delete("/path/to/file")

boolean isFile = exec.isFile("/path/to/check")
boolean isDir = exec.isDir("/path/to/check")
String[] files = exec.list("/path/to/dir")
```

`putFiles`/`getFiles` 在本地执行器为空操作，远程（SSH）通过 SFTP 传输，详见 `system2.md`。
