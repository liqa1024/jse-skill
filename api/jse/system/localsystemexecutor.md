# LocalSystemExecutor

> `jse.system.LocalSystemExecutor`

**核心职能**：`extends AbstractSystemExecutor`。通过 `ProcessBuilder` 在本地执行命令。自动并行读取进程 stdout/stderr 流（防死锁）。`LocalSystemFuture` 封装进程生命周期（超时、取消 `Process.destroy()`、doFinal 回调）。put/get 文件在本地为空操作。

**可覆写钩子**:

```java
protected String @NotNull[] programAndArgs_() → ZL_STR   // 命令前缀 (如 {"bash","-c"})
protected Charset charset_() → Charset.defaultCharset()   // 输出流字符集
```

```java
LocalSystemExecutor()                                // 构造器
ISystemExecutor setWorkingDir(@Nullable String)      // 设置 ProcessBuilder 工作目录
void validPath/makeDir/removeDir/delete/isFile/isDir/list(...)  // 直接委托 IO 静态方法
```
