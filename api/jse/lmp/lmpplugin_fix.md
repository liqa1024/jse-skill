# LmpPlugin.Fix

> `jse.lmp.LmpPlugin.Fix`

**核心职能**：继承此类实现 LAMMPS `fix jse`。子类须实现 `setMask()` 返回感兴趣的回调时机位掩码，通过 C 指针直接访问 LAMMPS 内部数据。`LmpPlugin.Fix.of("MyFix", fixPtr, args)` 反射创建。

```java
// === 静态工厂 ===
static Fix of(String classNameOrPath, long fixPtr, String... args)

// === 必须实现的抽象方法 ===
abstract int setMask()           // 返回感兴趣的回调时机位掩码（INITIAL_INTEGRATE | PRE_FORCE | ...）

// === 可覆写回调（20+ 个，均有默认空实现） ===
void init()                      // fix 初始化
void setup(int vflag)            // MD setup
void minSetup(int vflag)         // Minimize setup
void close()                     // 析构
// MD 阶段回调
void initialIntegrate(int) / postIntegrate() / preExchange() / preNeighbor() / postNeighbor()
void preForce(int) / preReverse(int,int) / postForce(int) / finalIntegrate()
void endOfStep() / postRun()
// Minimize 阶段回调
void minPreExchange/PreNeighbor/PostNeighbor/PreForce/PreReverse/PostForce(int...)
// 通信
int packForwardComm(int, IntCPointer, DoubleCPointer, int, IntCPointer)
void unpackForwardComm(int, int, DoubleCPointer)
int packReverseComm(int, int, DoubleCPointer)
void unpackReverseComm(int, IntCPointer, DoubleCPointer)
// 输出
double computeScalar() / computeVector(int i) / computeArray(int i, int j)

// === final 方法 — 盒/域/原子/近邻 全套 C 指针访问（同 Pair 模式） ===
// 配置: setBoxChange/setNoChangeBox/setNevery/setEnergyGlobalFlag/setVirialGlobalFlag...
// 近邻: neighborRequestDefault/Full/Occasional...
// 原子: atomX/atomV/atomF/atomMask/atomTag/atomType/atomMass...
// 域: domainXy/domainXprd/domainH/domainBoxlo/domainX2lamda/domainLamda2x/domainSetGlobalBox...
// 力场: forceBoltz/dt/ntimestep/firststep/laststep...
// 通信: commMe/commNprocs/commBarrier/commWorld...

// === 位掩码常量 ===
static final int INITIAL_INTEGRATE=1, POST_INTEGRATE=2, PRE_EXCHANGE=4, PRE_NEIGHBOR=8,
    POST_NEIGHBOR=16, PRE_FORCE=32, PRE_REVERSE=64, POST_FORCE=128, FINAL_INTEGRATE=256,
    END_OF_STEP=512, POST_RUN=1024
// Minimize 位掩码: MIN_PRE_EXCHANGE=1<<16, ..., MIN_POST_FORCE=1<<21

// === 盒变换常量 ===
static final int NO_BOX_CHANGE=0, BOX_CHANGE_ANY=1, BOX_CHANGE_DOMAIN=2,
    BOX_CHANGE_X=4, BOX_CHANGE_Y=8, BOX_CHANGE_Z=16,
    BOX_CHANGE_YZ=32, BOX_CHANGE_XZ=64, BOX_CHANGE_XY=128,
    BOX_CHANGE_SIZE=(X|Y|Z), BOX_CHANGE_SHAPE=(YZ|XZ|XY)
```
