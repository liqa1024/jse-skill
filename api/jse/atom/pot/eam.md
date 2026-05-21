# EAM

> `jse.atom.pot.EAM`

**核心职能**：`implements IPairPotential`。EAM 势函数 `E = ΣF(ρ) + ½Σφ(r)`，支持 eam/alloy/fs/adp 四种 DYNAMO 格式。使用样条插值（Linear/Fast 两种），半近邻列表。`new EAM("file.eam")` / `new EAM("file.eam", "format")`。

```java
// 构造器
EAM(String filePath, String format)  // 指定格式（eam/alloy/fs/adp）
EAM(String filePath)                 // 自动检测

// 配置内部类
static class Conf {
    static boolean USE_LAMMPS_PRECISION   // 使用 lammps 精度（默认 false）
    static boolean USE_SPLINE              // 使用样条插值（默认 true）
}

// IPairPotential 实现
int ntypes()                         // 元素种类数
boolean hasSymbol()                  // true
String symbol(int)                   // 元素符号
double rcutMax()                     // 最大截断半径
boolean manybody()                   // true（多体势）
boolean neighborListChecked()        // true
boolean neighborListHalf()           // true
int nthreads()
EAM setNthreads(int)
void calEnergy(int, INeighborListGetter, IEnergyAccumulator)
void calEnergyForceVirial(int, INeighborListGetter, IEnergyAccumulator?, IForceAccumulator?, IVirialAccumulator?)

// 文件写入
void write(String filePath, String format)
void write(String filePath)          // 默认 eam 格式

// @ApiStatus.Experimental — 势函数分量检查
@ApiStatus.Experimental IFunc1 frho(int type)          // 嵌入能 F(ρ)
@ApiStatus.Experimental IFunc1 rhor(int typeI, int typeJ) // 密度 ρ(r)
@ApiStatus.Experimental IFunc1 rphir(int typeI, int typeJ) // 对势 φ(r)
@ApiStatus.Experimental IFunc1 ur(int typeI, int typeJ)  // ADP dipolar (可能 null)
@ApiStatus.Experimental IFunc1 wr(int typeI, int typeJ)  // ADP quadrupolar (可能 null)
// 各函数均有对应的 Spline() 和 GradSpline() 版本
```
