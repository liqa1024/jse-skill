# OS.Slurm

> `jse.code.OS.Slurm`

**核心职能**：读取 SLURM 环境变量并暴露资源信息，提供智能资源分配器（优先单节点分配），以及 srun 指令生成。静态内部类，不实例化。

```java
static class Slurm {
    final static boolean IS_SLURM              // 是否 SLURM 环境
    final static boolean IS_SRUN               // 是否在 srun 中运行
    final static int PROCID                    // SLURM_PROCID
    final static int NTASKS                    // SLURM_NTASKS
    final static int CORES_PER_NODE            // 每节点核心数
    final static int CORES_PER_TASK            // 每任务核心数（-1 未设置）
    final static int MAX_STEP_COUNT            // 单任务最大作业步数，默认 40000
    final static int STEP_ID                   // SLURM_STEP_ID
    final static int JOB_ID                    // SLURM_JOB_ID
    final static String JOB_NAME               // SLURM_JOB_NAME
    final static int NODEID                    // SLURM_NODEID
    final static String NODENAME               // SLURMD_NODENAME
    final static List<String> NODE_LIST        // 分配到的节点列表
    final static ResourcesManager RESOURCES_MANAGER

    // 资源管理器：智能分配（优先单节点）、归还、生成 srun 指令
    final static class ResourcesManager {
        synchronized @Nullable Resource assignResource(int aTaskNum) // 按核数分配
        synchronized @Nullable Resource assignResource()             // 自动分配
        synchronized void returnResource(@NotNull Resource aResource)// 归还
        synchronized @Nullable String creatJobStep(@NotNull Resource aResource, String aCommand)
    }

    // 资源结构体
    final static class Resource {
        final @Unmodifiable List<String> nodelist    // 分配的节点列表
        final int nodes                              // 节点数
        final int ntasks                             // 总任务数
        final int ntasksPerNode                      // 每节点任务数
        final int[] ntasksPerNodeList                // 每节点任务数明细（内部使用）
    }
}
```
