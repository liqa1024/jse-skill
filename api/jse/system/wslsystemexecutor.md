# WSLSystemExecutor

> `jse.system.WSLSystemExecutor`

**核心职能**：final class extends AbstractSystemExecutor。WSL (Windows Subsystem for Linux) Bash 命令执行器，通过 `wsl bash -c` 执行命令。

```java
WSLSystemExecutor()               // programAndArgs_→{"wsl","bash","-c"}
```
