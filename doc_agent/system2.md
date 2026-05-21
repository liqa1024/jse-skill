# jse — 进阶系统命令

SLURM 集群资源分配与高通量任务提交、SSH 远程执行。本地基本执行器见 `system.md`。

> **类引用**：`OS.Slurm`=`jse.code.OS.Slurm`，`SRUN`=`jse.system.SRUN`，`SSH`=`jse.system.SSH`，`UT.Par`=`jse.code.UT.Par`

## SLURM 集成

jse 通过 `OS.Slurm` 读取 SLURM 环境变量，通过 `SRUN` 执行器在 SLURM 分配内提交 job steps，配合 `parfor` 实现高通量任务调度。

### 环境检测与信息

```groovy
OS.Slurm.IS_SLURM      // 是否在 SLURM 环境中（sbatch/salloc/srun）
OS.Slurm.NTASKS        // 任务总数
OS.Slurm.NODEID        // 当前节点编号（0-based）
OS.Slurm.NODE_LIST     // 分配到的节点列表
```

其余字段（`JOB_ID`、`CORES_PER_NODE`、`NODENAME` 等）查 `api/jse/code/os_slurm.md`。

### 高通量任务提交

`SRUN` 构造时预分配资源，配合 `UT.Par.parfor` 实现高通量任务调度。每个迭代中自动分配节点资源、生成 srun job step 并提交，任务完成后自动归还资源。优先将单个任务的所有核分配到同一节点避免跨节点通信，单节点不足时自动增加节点数重试。

```groovy
// job.groovy
int coresPerJob = args.length > 0 ? (args[0] as int) : 4
int parallel = (OS.Slurm.NTASKS / coresPerJob).intValue()
assert OS.Slurm.NTASKS % coresPerJob == 0 : "NTASKS (${OS.Slurm.NTASKS}) must be divisible by coresPerJob ($coresPerJob)"
assert parallel > 0 : "NTASKS (${OS.Slurm.NTASKS}) must be >= coresPerJob ($coresPerJob)"

int njobs = 100

def srun = new SRUN(coresPerJob, parallel)
UT.Par.parfor(njobs, parallel) { jobid ->
    // 自动分配资源并提交: srun -n $coresPerJob --nodelist ... <command>
    srun.system("echo Job $jobid running on host: \$(hostname)")
}
```

对于实际模拟任务（如 LAMMPS），常见模式是在 Groovy 中按 `jobid` 生成对应输入文件，`srun.system` 提交计算，完成后解析输出并清理临时文件。

SLURM 参数写入 `job.sh`，通过 `sbatch` 提交：

```bash
#!/bin/bash
#SBATCH -n 32
#SBATCH -N 1
jse job.groovy
```

```bash
sbatch job.sh
```

构造时预分配 `parallel` 个资源块（各含 `coresPerJob` 核），分配失败则直接报错。无参构造 `SRUN()` 取当前最大空闲单节点的全部剩余核数。

多节点提交时，`#SBATCH -N` 需确保各节点核数能被 `coresPerJob` 整除（单个任务不跨节点）：

```bash
#SBATCH -N 2
#SBATCH -n 64
#SBATCH --ntasks-per-node 32
```

脚本也可通过 `#!/usr/bin/env jse` shebang + LF 换行由 `sbatch` 直接执行，此时 `#SBATCH` 参数需在 `sbatch` 命令行中指定（Groovy 不支持 shebang 后续行的 `#` 注释）。

## SSH — 远程执行

`SSH` 通过 JSch 库连接远程服务器。文件系统操作（`validPath`/`makeDir`/`isFile`/`isDir`/`list`）通过 SFTP 在远端执行，`putFiles`/`getFiles` 实际跨网络传输。构造失败自动 `close()`。

### Map 构造

使用 Groovy Map 构造 `SSH`：

| Key | 简写 | 默认值 | 说明 |
|---|---|---|---|
| `hostname` | `h` | 必填 | 远程服务器地址 |
| `username` | `u` | 必填 | SSH 用户名 |
| `password` | `pw` | — | 密码认证（与 key 二选一） |
| `key` | `k` | `~/.ssh/id_rsa` | 密钥路径（与 password 二选一） |

其余参数（`port`、`compresslevel`）查 `api/jse/system/ssh.md`。

```groovy
// 密码连接
SSH ssh = new SSH([
    hostname: "cluster.univ.edu",
    username: "user",
    password: "your_password"
])
```

### 免密连接

通过 `key` 指定私钥路径，不传 `password` 即使用密钥认证：

```groovy
// 默认密钥 ~/.ssh/id_rsa
SSH ssh = new SSH([
    hostname: "cluster.univ.edu",
    username: "user"
])

// 指定密钥路径
SSH ssh = new SSH([
    hostname: "cluster.univ.edu",
    username: "user",
    key: "~/.ssh/cluster_rsa"
])
```

### 远程执行与文件传输

使用 `setLocalWorkingDir`/`setRemoteWorkingDir` 配置两端工作目录，之后 `putFiles`/`getFiles` 以**相对路径**（统一 `/` 分隔）基于此目录传输。路径在本地和远程两端共享，因此不能使用含盘符的绝对路径拼接：

```groovy
SSH ssh = new SSH([hostname: "cluster.univ.edu", username: "user", key: "~/.ssh/id_rsa"])
ssh.setLocalWorkingDir(OS.WORKING_DIR)
ssh.setRemoteWorkingDir("/home/user/sim/")

ssh.putFiles("input.txt", "params.json")
int ret = ssh.system("./run.sh")
List<String> output = ssh.system_str("squeue -u \$USER")
ssh.getFiles("result.csv")
```

`setCompressLevel` 可启用 zlib 压缩（减少传输量，增加 CPU 开销），`setBeforeCommand` 设置每次命令前自动执行的前置环境加载命令。

### 相对路径

`putFiles`/`getFiles` 路径在两端共享，需统一 `/` 分隔。日常使用中直接传文件名即可，需要从外部绝对路径传入时：

```groovy
// 任意绝对路径转为相对路径（同时 \ 统一替换为 /）
String relPath = IO.toRelativePath("/home/user/data/input.txt")

// 也可直接获取相对路径的临时工作目录
String tmpDir = Conf.WORKING_DIR_OF(UT.Code.randID(), true)
```

### 从配置文件读取

通过 `IO.json2map` 从 JSON 文件加载连接参数，结合 git 排除的目录（如 `.secret/`）避免凭证写入仓库：

```groovy
// .secret/ssh_config.json（已 gitignore）
// {"hostname":"cluster.univ.edu","username":"user","key":"~/.ssh/id_rsa"}

Map config = IO.json2map(".secret/ssh_config.json")
SSH ssh = new SSH(config)
ssh.setRemoteWorkingDir("/home/user/sim/")

ssh.system("sbatch job.sh")
```

> `ISystemExecutor` 通过 `ReferenceChecker` 在对象被 GC 时自动释放，Groovy 脚本无需手动关闭。详见 `system.md` 资源释放节。
