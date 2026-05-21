# SystemLmpPotential

> `jse.lmp.SystemLmpPotential`

**核心职能**：`extends AbstractLmpPotential`。通过系统命令启动独立 `lmp` 进程执行计算，兼容性高（任意 LAMMPS 版本）但效率较低。线程安全。`new SystemLmpPotential("pair_style", "pair_coeff")` / `new SystemLmpPotential("eam", "Ni", OS.EXEC)`。

```java
// === 构造器 ===
SystemLmpPotential(String, String[], ISystemExecutor, boolean closeExec)  // 主构造
SystemLmpPotential(String, String, ISystemExecutor, boolean)
SystemLmpPotential(String, Collection, ISystemExecutor, boolean)
SystemLmpPotential(String, String[], ISystemExecutor)        // closeExec=true
SystemLmpPotential(String, String, ISystemExecutor)
SystemLmpPotential(String, Collection, ISystemExecutor)
SystemLmpPotential(String pairStyle, String... pairCoeff)    // 使用 OS.EXEC

// === 配置 ===
SystemLmpPotential setLmpCommand(String)                     // 设置 lmp 命令，默认 "lmp"

// === 生命周期 ===
boolean isClosed()
void close() throws Exception                                // 清理临时文件，按需关闭 ISystemExecutor

// === 核心计算 ===
void calEnergyForceVirials(IAtomData, ...) throws IOException  // 不支持 9 分量维里
// 继承 AbstractLmpPotential 的全部 set* 方法
```
