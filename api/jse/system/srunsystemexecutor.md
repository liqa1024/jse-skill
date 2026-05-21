# SRUNSystemExecutor

> `jse.system.SRUNSystemExecutor`

**核心职能**：`extends LocalSystemExecutor`。在 SLURM 环境中提交子任务（srun job steps）。构造时通过 `RESOURCES_MANAGER` 预分配资源块（优先单节点，不足时自动跨节点重试）。`submitSystem__` 将命令写入临时 `.sh` 脚本由 `bash` 执行，`SRUNSystemFuture` 嵌套 `LocalSystemFuture`，完成时自动归还资源。`SRUNChecker`（`ReferenceChecker` 子类）在 GC 时自动清理临时目录并归还全部预分配资源。

```java
// aTaskNum: 每任务核数（-1 → 自动取最大空闲单节点核数）
// aMaxParallelNum: 并行槽数，构造时预分配对应数量的资源块，任一块分配失败则抛异常
SRUNSystemExecutor(int aTaskNum, int aMaxParallelNum)
SRUNSystemExecutor(int aTaskNum)                        // → (aTaskNum, 1)
SRUNSystemExecutor()                                    // → (-1, 1)
```
