# LmpPlugin.Pair

> `jse.lmp.LmpPlugin.Pair`

**核心职能**：继承此类实现 LAMMPS `pair_style jse`。在 Groovy 脚本中定义 `compute()`/`coeff(String...)/initOne(int,int)` 即可创建自定义对势。通过 C 指针直接访问 LAMMPS 内部数据结构。`LmpPlugin.Pair.of("MyPair", pairPtr)` 反射创建。

```java
// === 静态工厂 ===
static Pair of(String classNameOrPath, long pairPtr)  // 通过类名或 .groovy 文件路径反射创建
static int sbmask(int j)                               // 获取特殊键掩码

// === 必须实现的抽象方法 ===
abstract void compute()                                // 核心：pair 计算主逻辑
abstract void coeff(String... args)                    // pair_coeff 回调
abstract double initOne(int i, int j)                  // 初始化种类对，返回截断半径

// === 可覆写方法（均有默认空实现） ===
double single(int i, int j, int itype, int jtype, double rsq,
    double factor_coul, double factor_lj, DoubleCPointer fforce)  // 每对作用计算
void settings(String... args)                               // pair_style 回调
void initStyle()                                            // pair 初始化
void close()                                                // 析构
int packForwardComm(int n, IntCPointer list, DoubleCPointer buf, int pbc, IntCPointer)  // 前向通信打包
void unpackForwardComm(int n, int first, DoubleCPointer buf)   // 前向通信解包
int packReverseComm(int n, int first, DoubleCPointer buf)     // 反向通信打包
void unpackReverseComm(int n, IntCPointer list, DoubleCPointer buf)  // 反向通信解包

// === final 方法 — 原子数据 C 指针 ===
final NestedDoubleCPointer atomX()    // 位置 [natoms][3]
final NestedDoubleCPointer atomV()    // 速度
final NestedDoubleCPointer atomF()    // 力
final IntCPointer atomTag()           // tag
final IntCPointer atomType()          // type
final DoubleCPointer atomMass()       // mass
final CPointer atomExtract(String)    // 通用属性指针
final long atomNatoms()               // 总原子数
final int atomNtypes/atomNlocal/atomNghost/atomNmax()

// === final 方法 — 近邻列表 C 指针 ===
final IntCPointer listIlist()                          // ilist
final IntCPointer listNumneigh()                       // numneigh
final NestedIntCPointer listFirstneigh()               // firstneigh[nlocal][]
final double cutsq(int i, int j)                       // 种类对截断距离平方

// === final 方法 — 能量/维里 C 指针与统计 ===
final DoubleCPointer engVdwl(), engCoul(), eatom()     // 能量指针
final DoubleCPointer virial()                          // 全局维里
final NestedDoubleCPointer vatom()                     // 原子维里 [natoms][6]
final NestedDoubleCPointer cvatom()                    // 质心维里
final void evTally(int i, int j, int nlocal, boolean newton, double evdwl, double ecoul, double fpair, double delx, double dely, double delz)
final void evTallyFull(int i, double evdwl, double ecoul, double fpair, double delx, double dely, double delz)
final void evTallyXYZ(...) / evTallyXYZFull(...)
final boolean evflag(), vflagEither(), vflagGlobal(), vflagAtom(), cvflagAtom()
final boolean eflagEither(), eflagGlobal(), eflagAtom()

// === final 方法 — 配置 ===
final void setSingleEnable(boolean) / setOneCoeff(boolean) / setManybodyFlag(boolean)
final void setCentroidstressflag(int) / setCommForward(int) / setCommReverse(int)
final void neighborRequestDefault() / neighborRequestFull()
final int neighborAgo()

// === final 方法 — 通信 ===
final int commMe() / commNprocs()
final void commBarrier()
final MPI.Comm commWorld()
final void commForwardComm/commReverseComm()
final String unitStyle()
```
