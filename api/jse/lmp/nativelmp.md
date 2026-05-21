# NativeLmp

> `jse.lmp.NativeLmp`

**核心职能**：`implements AutoCloseable`。基于 JNI 的 LAMMPS C 库完整封装，类似 Python lammps 模块。提供命令执行、原子数据提取/设置、compute 属性、盒操作、数据加载/导出。**线程绑定**（创建和访问须同一线程）。`new NativeLmp()` / `new NativeLmp(args...)` / `new NativeLmp(MPI.Comm)`。

```java
// === 构造器 ===
NativeLmp(String[] args, MPI.Comm)                           // 主构造
NativeLmp(MPI.Comm, String... args)
NativeLmp(Collection<? extends CharSequence>, MPI.Comm)
NativeLmp(String... args)                                     // MPI=null
NativeLmp(MPI.Comm)
NativeLmp()                                                   // 无参

// === 常量 ===
static final int LMP_STYLE_GLOBAL=0, ATOM=1, LOCAL=2
static final int LMP_TYPE_SCALAR=0, VECTOR=1, ARRAY=2
static final int LMP_SIZE_VECTOR=3, SIZE_ROWS=4, SIZE_COLS=5
static final boolean LAMMPS_LIB_MPI, LAMMPS_BIGBIG

// === 线程安全 ===
boolean threadValid()                                         // 当前线程是否为创建线程
void checkThread()                                            // 不一致时抛 LmpException

// === 命令执行 ===
void command(String)                                          // 执行单条 LAMMPS 命令
void commands(String... cmds)                                 // 执行多条命令
void commands(String multiCmd)                                // 执行多行命令块
void file(String path)                                        // 从文件读取并执行 LAMMPS 命令

// === 查询 ===
boolean hasStyle(String category, String name)                // 查询 style 是否可用
int version()                                                 // LAMMPS 数值版本
String versionStr()                                           // LAMMPS 字符串版本
MPI.Comm comm()                                               // MPI 通信域

// === 原子/系统信息 ===
long natoms()                                                 // 总原子数
int ntypes(), nlocal(), nghost()                              // 种类数/本地原子/ghost原子

// === 盒操作 ===
LmpBox box()                                                  // 提取当前模拟盒
void resetBox(double xlo, xhi, ylo, yhi, zlo, zhi, xy, xz, yz)  // 重置三斜盒
void resetBox(double xlo, xhi, ylo, yhi, zlo, zhi)            // 重置正交盒
void resetBox(double xhi, yhi, zhi)                           // 从原点重置
void resetBox(LmpBoxPrism) / resetBox(LmpBox)                // 从 LAMMPS 盒重置
void resetBox(IXYZ lo, IXYZ hi) / resetBox(IXYZ)             // 从向量重置

// === Thermo / Setting ===
double thermoOf(String name)                                  // 获取 thermo 关键字值
int settingOf(String name)                                    // 获取全局设置整数值

// === 原子数据提取 ===
RowMatrix atomDataOf(String name)                             // 按名称自动检测类型
RowIntMatrix atomIntDataOf(String name)                       // 整数类型原子数据
RowMatrix fullAtomDataOf(String name, boolean isDouble, int colNum) // 显式类型
RowMatrix localAtomDataOf(String, int dataType, int rows, int cols) // 本进程数据
CPointer localAtomCPointerDataOf(String name)                 // 直接 C 指针（避免拷贝）

// === Compute 属性 ===
RowMatrix computeOf(String name, int dataStyle, int dataType)  // 获取 compute 值
int computeSizeOf(String name, int dataStyle, int dataType)    // compute 属性大小
CPointer computeCPointerOf(String name, int dataStyle, int dataType) // C 指针

// === 原子数据设置 ===
void setAtomDataOf(String name, IMatrix data)
void setAtomDataOf(String name, IMatrix data, boolean isDouble)

// === 质量 ===
IVector masses()                                              // 所有种类质量向量
double mass(int type)                                         // 指定种类质量

// === 数据加载/导出 ===
Lmpdat lmpdat() / lmpdat(boolean noVelocities)               // 导出为 Lmpdat
void loadLmpdat(Lmpdat, boolean discardID)                    // 加载 Lmpdat
void loadData(IAtomData, boolean discardID)                   // 从 IAtomData 加载
void creatAtoms(List<? extends IAtom>, boolean shrink, boolean discardID)
void clear()                                                  // lammps clear
void close()                                                  // 关闭 LAMMPS 实例
@VisibleForTesting Lmpdat data()                                     // :note: Groovy 脚本优先使用 data() 代替 lmpdat()
@VisibleForTesting Lmpdat data(boolean noVelocities)                 // :note: Groovy 脚本优先使用 data(boolean) 代替 lmpdat(boolean)

// === 插件 ===
void loadPlugin()                                             // 加载 LmpPlugin
boolean hasPlugin()                                           // 是否已加载

// === 全局生命周期（静态） ===
static void initMPI() / closeMPI() / closeKokkos() / closePlugin() / closePython()
static void closeAll()                                        // Kokkos+Python+Plugin+MPI
```
