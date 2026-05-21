# CMDSystemExecutor

> `jse.system.CMDSystemExecutor`

**核心职能**：final class extends AbstractSystemExecutor。Windows 命令提示符执行器，通过 `cmd /c` 执行命令，默认字符集 GBK。

```java
CMDSystemExecutor()               // programAndArgs_→{"cmd","/c"}, charset_→GBK
```
