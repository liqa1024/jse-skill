# PWSHSystemExecutor

> `jse.system.PWSHSystemExecutor`

**核心职能**：final class extends AbstractSystemExecutor。PowerShell Core (pwsh) 执行器，命令经 Base64 编码后通过 `-EncodedCommand` 传入。

```java
PWSHSystemExecutor()              // Program: pwsh -of Text -ec, 同 Base64 编码
```
