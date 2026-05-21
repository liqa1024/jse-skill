# SRUN

> `jse.system.SRUN`

**核心职能**：`@VisibleForTesting`，`final`，`extends SRUNSystemExecutor`。

```java
SRUN(int aTaskNum, int aParallelNum) throws Exception
SRUN(int aTaskNum) throws Exception   // → (aTaskNum, 1)
SRUN() throws Exception               // → (-1, 1)
```
