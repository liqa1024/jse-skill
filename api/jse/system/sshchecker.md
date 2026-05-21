# SSHChecker

> `jse.system.SSHChecker`

> 此类为 @ApiStatus.Internal / package-private

**核心职能**：`extends ReferenceChecker`。自动回收 `SSHSystemExecutor` 内部 `SSHCore`。GC 时执行 `close()`，每次创建前清理旧数据。

```java
// === 构造器 ===
SSHChecker(SSHSystemExecutor, SSHCore)

// === ReferenceChecker 接口实现 ===
protected void dispose_()
```
