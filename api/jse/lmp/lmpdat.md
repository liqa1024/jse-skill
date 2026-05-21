# Lmpdat

> `jse.lmp.Lmpdat`

**核心职能**：`extends AbstractSettableAtomData`。LAMMPS `write_data` 格式的完整实现，存储原子 ID/type/坐标/速度/键（bond）及模拟盒，支持文件读写、MPI 通信。`Lmpdat.read(file)` / `Lmpdat.of(IAtomData)` / `Lmpdat.of(IAtomData, double... masses)`。

> **`Data`**（extends Lmpdat）为 `@VisibleForTesting` 别名，无新增方法。

```java
// === 列索引常量 ===
final static int LMPDAT_ID_COL=0, TYPE_COL=1, X_COL=2, Y_COL=3, Z_COL=4     // atomic style
final static int LMPDAT_VX_COL=1, VY_COL=2, VZ_COL=3                         // Velocity 列
final static int LMPDAT_FULL_ID_COL=0, FULL_TYPE_COL=1, FULL_MOL_COL=2, FULL_CHARGE_COL=3, FULL_X_COL=4, FULL_Y_COL=5, FULL_Z_COL=6
final static int LMPDAT_BOND_ID_COL=0, BOND_TYPE_COL=1, BOND_ID1_COL=2, BOND_ID2_COL=3

// === 静态工厂 ===
static Lmpdat read(String filePath) throws IOException
static Lmpdat read(BufferedReader) throws IOException
static Lmpdat of(IAtomData)                                  // 自动质量
static Lmpdat of(IAtomData, double... masses)                // 变长参数指定质量
static Lmpdat of(IAtomData, IVector masses)                  // 向量指定质量
static Lmpdat of(IAtomData, Collection<? extends Number>)    // 集合指定质量

// === 数据访问 ===
IntVector ids()                           // 原子 ID 向量
IntVector types()                         // 原子 type 向量
RowMatrix positions()                     // 坐标矩阵 (natoms × 3)
@Nullable RowMatrix velocities()          // 速度矩阵（null if !hasVelocity）
ISettableAtom atom(int aIdx)              // 含键信息的可设置原子引用
LmpBox box()                              // 模拟盒
int natoms()                              // 原子总数
int ntypes()                              // 原子种类数
int ntypesBond()                          // 键种类数
boolean hasID() → true                    // Lmpdat 始终包含 ID
boolean hasBond()                         // 是否包含键信息
boolean hasBondID()                       // 键是否包含 ID
boolean hasVelocity()                     // 是否包含速度
boolean hasMass()                         // 是否包含质量（≡ hasSymbol）
boolean hasSymbol()                       // 是否包含元素符号
@Nullable String symbol(int aType)        // 指定种类的符号
double mass(int aType)                    // 指定种类的质量（不存在返回 NaN）

// === 修改（返回 this 链式） ===
Lmpdat setNtypes(int)                     // 设置种类数（可截断/扩容）
Lmpdat setNtypesBond(int)                 // 设置键种类数
Lmpdat setNoVelocity()                    // 清除速度
Lmpdat setHasVelocity()                   // 启用速度（初始化为零矩阵）
Lmpdat setMasses(double... masses)        // 变长参数设置质量
Lmpdat setMasses(Collection<? extends Number>)
Lmpdat setMasses(@Nullable IVector)
Lmpdat setNoMass()                        // 清除质量
Lmpdat setSymbolOrder(String...)           // 重新排列种类顺序
Lmpdat setSymbols(String...)               // 设置种类名称

// === 缓存管理 ===
boolean isFromCache()                     // 内部数据是否来自缓存池
void returnToCache()                      // 归还到缓存池

// === 文件 I/O ===
void write(String filePath) throws IOException
void write(IO.IWriteln) throws IOException
Lmpdat copy()

// === MPI 通信（静态） ===
static void send(Lmpdat, int dest, MPI.Comm) throws MPIException
static Lmpdat recv(int src, MPI.Comm) throws MPIException
static Lmpdat bcast(Lmpdat, int root, MPI.Comm) throws MPIException
```
