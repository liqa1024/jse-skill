# PowerShellSystemExecutor

> `jse.system.PowerShellSystemExecutor`

**核心职能**：命令经 Base64(UTF-16LE) 编码后通过 `-EncodedCommand` 传入，避免转义问题。

```java
PowerShellSystemExecutor()        // Program: PowerShell -OutputFormat Text -EncodedCommand
// 覆写 submitSystem__: Base64.getEncoder().encode(aCommand.getBytes(UTF_16LE))
```
