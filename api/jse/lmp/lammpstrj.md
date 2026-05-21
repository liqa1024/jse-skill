# Lammpstrj

> `jse.lmp.Lammpstrj`

**核心职能**：`extends AbstractListWrapper<SubLammpstrj, IAtomData, SubLammpstrj>`。多帧 LAMMPS dump 原子数据容器，支持文件读写、帧截取/采样、MPI 通信、Groovy `dump[i]` 索引。`Lammpstrj.read(file)` / `Lammpstrj.of(IAtomData)` / `Lammpstrj.zl()`。

> **`Dump`**（final extends Lammpstrj）为 `@VisibleForTesting` 别名，构造器 private。

```java
// === 静态工厂 ===
static Lammpstrj read(String filePath) throws IOException
static Lammpstrj read(BufferedReader) throws IOException
static Lammpstrj zl()                                        // 空容器
static Lammpstrj of(IAtomData)                               // 单帧，自动时间步
static Lammpstrj of(IAtomData, long timeStep)                // 单帧，指定时间步
static Lammpstrj of(Iterable<? extends IAtomData>)           // 多帧 Iterable
static Lammpstrj of(Iterable, ILongVectorGetter timeSteps)  // 多帧+自定义时间步
static Lammpstrj of(Collection<? extends IAtomData>)         // 多帧 Collection
static Lammpstrj of(Collection, ILongVectorGetter timeSteps)
static Lammpstrj of(AbstractListWrapper<? extends IAtomData, ?, ?>)  // 直接包装

// === 数据操作 ===
Lammpstrj append(IAtomData)                                   // 追加一帧（自动时间步）
Lammpstrj append(IAtomData, long timeStep)                    // 追加一帧（指定时间步）
Lammpstrj appendAll(Collection<? extends IAtomData>)          // 批量追加
Lammpstrj appendFile(String filePath) throws IOException      // 从文件追加
Lammpstrj leftShift(IAtomData)                                 // Groovy << 操作符
Lammpstrj leftShift(Collection<? extends IAtomData>)           // Groovy << 批量

// === 截取/采样 ===
Lammpstrj cutFront(int length)                                 // 保留前 N 帧
Lammpstrj cutBack(int length)                                  // 保留后 N 帧
Lammpstrj step(int aStep)                                      // 等间距采样

// === 文件 I/O ===
void write(String filePath) throws IOException
void write(IO.IWriteln) throws IOException
Lammpstrj copy()
List<ITable> asTables()                                        // 所有帧转为 ITable 列表

// === MPI 通信（静态） ===
static void send(Lammpstrj, int dest, MPI.Comm) throws MPIException
static Lammpstrj recv(int src, MPI.Comm) throws MPIException
static Lammpstrj bcast(Lammpstrj, int root, MPI.Comm) throws MPIException
static Lammpstrj gather(Lammpstrj, int root, MPI.Comm) throws MPIException
static Lammpstrj allgather(Lammpstrj, MPI.Comm) throws MPIException
static Lammpstrj scatter(Lammpstrj, int root, MPI.Comm) throws MPIException
```
