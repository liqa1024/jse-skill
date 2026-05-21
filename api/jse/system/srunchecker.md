# SRUNChecker

> `jse.system.SRUNChecker`

> 此类为 @ApiStatus.Internal / package-private

**核心职能**：`extends ReferenceChecker`。自动回收 `SRUNSystemExecutor` 创建的临时文件夹及预分配 SLURM 资源。GC 时执行清理，每次创建前清理旧数据。

```java
// === 构造器 ===
SRUNChecker(SRUNSystemExecutor, Map<Slurm.Resource, Boolean>)

// === ReferenceChecker 接口实现 ===
protected void dispose_() throws IOException
```
