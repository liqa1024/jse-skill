# MPI.Comm

> `jse.parallel.MPI.Comm`

**核心职能**：`static class implements AutoCloseable`。封装 MPI Communicator 句柄，所有集合通信与点对点通信的载体。预置 `WORLD`/`SELF`/`NULL` 静态实例。`copy()`/`create()`/`split()` 产生新通信器，`close()` 释放（仅释放派生通信器，不释放预置实例）。`group()` 获取关联进程组。

所有通信方法遵循统一的多重重载族：`IDataShell<?>` 壳层（自动推断类型/长度）→ 8 种基本类型数组（`byte`/`double`/`boolean`/`char`/`short`/`int`/`long`/`float`）→ CPointer 指针（`DoubleCPointer`/`FloatCPointer`/`IntCPointer`/`ICPointer`+`Datatype`）→ 标量便捷方法（后缀 `B`/`D`/`Z`/`C`/`S`/`I`/`L`/`F`）。

```java
static final Comm NULL, WORLD, SELF

// === 基础查询 ===
int rank() throws MPIException
int size() throws MPIException
Comm copy() throws MPIException
Comm create(Group aGroup) throws MPIException
Comm split(int aColor, int aKey) throws MPIException
Comm split(int aColor) throws MPIException
Group group() throws MPIException
void close() throws MPIException

// === Barrier (同步屏障) ===
void barrier() throws MPIException

// === Bcast (广播, root→all) ===
// 数组 — 支持 8 种基本类型
void bcast(byte[] rBuf, int aStart, int aCount, int aRoot)
void bcast(double[] rBuf, int aStart, int aCount, int aRoot)
// ... 其余 6 种类型完全相同的参数模式
// IDataShell 壳层
void bcast(IDataShell<?> rBuf, int aRoot)
// CPointer 指针 — DoubleCPointer/FloatCPointer/IntCPointer/ICPointer
void bcast(DoubleCPointer rBuf, int aCount, int aRoot)
void bcast(FloatCPointer rBuf, int aCount, int aRoot)
void bcast(IntCPointer rBuf, int aCount, int aRoot)
void bcast(ICPointer rBuf, int aCount, Datatype aDataType, int aRoot)
// 标量便捷方法 — 8 种
byte bcastB(byte aB, int aRoot) throws MPIException
double bcastD(double aD, int aRoot) throws MPIException
boolean bcastZ(boolean aZ, int aRoot) throws MPIException
char bcastC(char aC, int aRoot) throws MPIException
short bcastS(short aS, int aRoot) throws MPIException
int bcastI(int aI, int aRoot) throws MPIException
long bcastL(long aL, int aRoot) throws MPIException
float bcastF(float aF, int aRoot) throws MPIException
// String (内部序列化为 byte[] 传输)
String bcastStr(String aStr, int aRoot) throws MPIException

// === Gather (收集, all→root) ===
// 数组收发 — 8 种类型
void gather(byte[] aSendBuf, int aSendStart, byte[] rRecvBuf, int aRecvStart, int aCount, int aRoot)
void gather(double[] aSendBuf, int aSendStart, double[] rRecvBuf, int aRecvStart, int aCount, int aRoot)
// ... 其余 6 种类型完全相同的参数模式
// 数组 in-place — 8 种类型
void gather(byte[] rBuf, int aStart, int aCount, int aRoot)
// IDataShell 壳层
void gather(IDataShell<?> aSendBuf, IDataShell<?> rRecvBuf, int aRoot)
void gather(IDataShell<?> rBuf, int aRoot)
// CPointer 指针 — 4 种 send+recv + 4 种 in-place (Double/Float/Int/ICPointer)
void gather(DoubleCPointer aSendBuf, DoubleCPointer rRecvBuf, int aCount, int aRoot)
void gather(FloatCPointer aSendBuf, FloatCPointer rRecvBuf, int aCount, int aRoot)
void gather(IntCPointer aSendBuf, IntCPointer rRecvBuf, int aCount, int aRoot)
void gather(ICPointer aSendBuf, ICPointer rRecvBuf, int aCount, Datatype aDataType, int aRoot)

// === Gatherv (可变长收集, all→root, +int[] aCounts) ===
void gatherv(IDataShell<?> aSendBuf, IDataShell<?> rRecvBuf, int[] aCounts, int aRoot)
void gatherv(byte[] aSendBuf, int aSendStart, byte[] rRecvBuf, int aRecvStart, int[] aCounts, int aRoot)
// ... 所有 8 种类型收发/in-place + CPointer 变体

// === Scatter (分发, root→all) ===
void scatter(byte[] aSendBuf, int aSendStart, byte[] rRecvBuf, int aRecvStart, int aCount, int aRoot)
// ... 所有 8 种类型 + IDataShell + CPointer 变体

// === Scatterv (可变长分发, root→all, +int[] aCounts) ===
void scatterv(byte[] aSendBuf, int aSendStart, byte[] rRecvBuf, int aRecvStart, int[] aCounts, int aRoot)
// ... 所有 8 种类型 + IDataShell + CPointer 变体

// === Allgather (全收集, all↔all) ===
void allgather(byte[] aSendBuf, int aSendStart, byte[] rRecvBuf, int aRecvStart, int aCount)
// ... 所有 8 种类型 + IDataShell + CPointer 变体

// === Allgatherv (可变长全收集, +int[] aCounts) ===
void allgatherv(byte[] aSendBuf, int aSendStart, byte[] rRecvBuf, int aRecvStart, int[] aCounts)
// ... 所有 8 种类型 + IDataShell + CPointer 变体

// === Reduce (归约, all→root) ===
void reduce(byte[] aSendBuf, int aSendStart, byte[] rRecvBuf, int aRecvStart, int aCount, Op aOp, int aRoot)
void reduce(byte[] rBuf, int aStart, int aCount, Op aOp, int aRoot)
void reduce(IDataShell<?> aSendBuf, IDataShell<?> rRecvBuf, Op aOp, int aRoot)
void reduce(IDataShell<?> rBuf, Op aOp, int aRoot)
void reduce(DoubleCPointer aSendBuf, DoubleCPointer rRecvBuf, int aCount, Op aOp, int aRoot)
// ... FloatCPointer/IntCPointer/ICPointer 变体
// 标量便捷方法 — 8 种
byte reduceB(byte aB, Op aOp, int aRoot) throws MPIException
double reduceD(double aD, Op aOp, int aRoot) throws MPIException
boolean reduceZ(boolean aZ, Op aOp, int aRoot) throws MPIException
char reduceC(char aC, Op aOp, int aRoot) throws MPIException
short reduceS(short aS, Op aOp, int aRoot) throws MPIException
int reduceI(int aI, Op aOp, int aRoot) throws MPIException
long reduceL(long aL, Op aOp, int aRoot) throws MPIException
float reduceF(float aF, Op aOp, int aRoot) throws MPIException

// === Allreduce (全归约, all↔all) ===
void allreduce(byte[] aSendBuf, int aSendStart, byte[] rRecvBuf, int aRecvStart, int aCount, Op aOp)
// ... 所有 8 种类型 + IDataShell + CPointer + 8 标量便捷方法
byte allreduceB(byte aB, Op aOp) throws MPIException
double allreduceD(double aD, Op aOp) throws MPIException
boolean allreduceZ(boolean aZ, Op aOp) throws MPIException
char allreduceC(char aC, Op aOp) throws MPIException
short allreduceS(short aS, Op aOp) throws MPIException
int allreduceI(int aI, Op aOp) throws MPIException
long allreduceL(long aL, Op aOp) throws MPIException
float allreduceF(float aF, Op aOp) throws MPIException

// === Send (点对点发送) ===
void send(byte[] aBuf, int aStart, int aCount, int aDest, int aTag)
// ... 其余 7 种类型完全相同的参数模式
void send(int aDest, int aTag)
void send(IDataShell<?> aBuf, int aDest, int aTag)
void send(DoubleCPointer aBuf, int aCount, int aDest, int aTag)
void send(FloatCPointer aBuf, int aCount, int aDest, int aTag)
void send(IntCPointer aBuf, int aCount, int aDest, int aTag)
void send(ICPointer aBuf, int aCount, Datatype aDataType, int aDest, int aTag)
// 标量便捷方法 — 8 种
void sendB(byte aB, int aDest, int aTag) throws MPIException
void sendD(double aD, int aDest, int aTag) throws MPIException
void sendZ(boolean aZ, int aDest, int aTag) throws MPIException
void sendC(char aC, int aDest, int aTag) throws MPIException
void sendS(short aS, int aDest, int aTag) throws MPIException
void sendI(int aI, int aDest, int aTag) throws MPIException
void sendL(long aL, int aDest, int aTag) throws MPIException
void sendF(float aF, int aDest, int aTag) throws MPIException
void sendStr(String aStr, int aDest, int aTag) throws MPIException

// === Recv (点对点接收) ===
void recv(byte[] rBuf, int aStart, int aCount, int aSource, int aTag)
// ... 其余 7 种类型完全相同的参数模式
void recv(int aSource, int aTag)
void recv(IDataShell<?> rBuf, int aSource, int aTag)
void recv(DoubleCPointer rBuf, int aCount, int aSource, int aTag)
void recv(FloatCPointer rBuf, int aCount, int aSource, int aTag)
void recv(IntCPointer rBuf, int aCount, int aSource, int aTag)
void recv(ICPointer rBuf, int aCount, Datatype aDataType, int aSource, int aTag)
// 标量便捷方法 — 8 种 (有返回值)
byte recvB(int aSource, int aTag) throws MPIException
double recvD(int aSource, int aTag) throws MPIException
boolean recvZ(int aSource, int aTag) throws MPIException
char recvC(int aSource, int aTag) throws MPIException
short recvS(int aSource, int aTag) throws MPIException
int recvI(int aSource, int aTag) throws MPIException
long recvL(int aSource, int aTag) throws MPIException
float recvF(int aSource, int aTag) throws MPIException
String recvStr(int aSource, int aTag) throws MPIException

// === Sendrecv (同时收发, 不同 tag/source/dest) ===
void sendrecv(IDataShell<?> aSendBuf, int aDest, int aSendTag, IDataShell<?> rRecvBuf, int aSource, int aRecvTag)
void sendrecv(byte[] aSendBuf, int aSendStart, int aSendCount, int aDest, int aSendTag, byte[] rRecvBuf, int aRecvStart, int aRecvCount, int aSource, int aRecvTag)
// ... 全部 64 种 send/recv 类型组合 + 10 种 CPointer 组合
void sendrecv(DoubleCPointer aSendBuf, int aSendCount, int aDest, int aSendTag, DoubleCPointer rRecvBuf, int aRecvCount, int aSource, int aRecvTag)
void sendrecv(DoubleCPointer aSendBuf, int aSendCount, int aDest, int aSendTag, FloatCPointer rRecvBuf, int aRecvCount, int aSource, int aRecvTag)
// ... 其余 9 种 CPointer 组合 + ICPointer 变体
void sendrecv(ICPointer aSendBuf, int aSendCount, Datatype aSendType, int aDest, int aSendTag, ICPointer rRecvBuf, int aRecvCount, Datatype aRecvType, int aSource, int aRecvTag)

// === 内部 (JNI 桥接) ===
@ApiStatus.Internal static Comm of(long aPtr)
@ApiStatus.Internal long ptr_()
```
