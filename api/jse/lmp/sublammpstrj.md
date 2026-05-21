# SubLammpstrj

> `jse.lmp.SubLammpstrj`

**核心职能**：`extends AbstractSettableAtomData`。单帧 LAMMPS dump 原子数据，支持坐标类型自动识别（x/xs/xu/xsu）、box bounds、时间步、wrap/unwrap 操作。`SubLammpstrj.read(file)` / `SubLammpstrj.of(IAtomData)` / `SubLammpstrj.of(IAtomData, timeStep)`。

> **`SubDump`**（final extends SubLammpstrj）为 `@VisibleForTesting` 别名。

```java
// === 静态工厂 ===
static SubLammpstrj read(String filePath) throws IOException
static SubLammpstrj read(BufferedReader) throws IOException
static SubLammpstrj of(IAtomData)
static SubLammpstrj of(IAtomData, long timeStep)

// === 属性访问 ===
long timeStep()                                          // 当前帧时间步
String[] boxBounds()                                     // 盒边界类型 {"pp","pp","pp"}
ITable asTable()                                         // 转为 ITable 直接操作列

// === 属性修改 ===
SubLammpstrj setTimeStep(long)                           // 返回 this
SubLammpstrj setNtypes(int)

// === 核心 IAtomData 实现 ===
ISettableAtom atom(int aIdx)                             // 含坐标类型自动处理的原子
LmpBox box()                                             // LAMMPS 风格模拟盒
int natoms() / ntypes()
boolean hasID() / hasVelocity()
SubLammpstrj copy()

// === 文件 I/O ===
void write(String filePath) throws IOException
void write(IO.IWriteln) throws IOException

// === MPI 通信（静态） ===
static void send(SubLammpstrj, int dest, MPI.Comm) throws MPIException
static SubLammpstrj recv(int src, MPI.Comm) throws MPIException
static SubLammpstrj bcast(SubLammpstrj, int root, MPI.Comm) throws MPIException
```
