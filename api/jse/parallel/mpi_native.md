# MPI.Native

> `jse.parallel.MPI.Native`

**核心职能**：`static class`。暴露 MPI C API 的低级 JNI 方法层。所有方法直接接受 `long` 句柄（Comm/Group/Op/Datatype），可通过 `import static MPI.Native.*` 直接使用 C 风格 API。`static final` 常量字段在静态初始化时通过 JNI 从 C 头文件 `#define` 值加载。生命周期、通信器、进程组方法为独立 `native` 方法；集合通信与点对点方法的高层重载（数组/指针/标量）与 `MPI.Comm` ——对应（参数中 `Op`→`long aOp`、`Datatype`→`long aDataType`、`Comm`→`long aComm`），底层委托 `private native` 方法。

```java
// === 常量 (JNI 从 C 头文件加载) ===
static final long MPI_GROUP_NULL, MPI_GROUP_EMPTY
static final long MPI_COMM_NULL, MPI_COMM_WORLD, MPI_COMM_SELF
static final long MPI_OP_NULL, MPI_MAX, MPI_MIN, MPI_SUM, MPI_PROD
static final long MPI_LAND, MPI_BAND, MPI_LOR, MPI_BOR, MPI_LXOR, MPI_BXOR
static final long MPI_MINLOC, MPI_MAXLOC, MPI_REPLACE
static final long MPI_DATATYPE_NULL
static final long MPI_CHAR, MPI_UNSIGNED_CHAR, MPI_SHORT, MPI_UNSIGNED_SHORT
static final long MPI_INT, MPI_UNSIGNED, MPI_LONG, MPI_UNSIGNED_LONG
static final long MPI_LONG_LONG, MPI_FLOAT, MPI_DOUBLE, MPI_BYTE, MPI_SIGNED_CHAR
static final long MPI_UNSIGNED_LONG_LONG
static final long MPI_INT8_T, MPI_INT16_T, MPI_INT32_T, MPI_INT64_T
static final long MPI_UINT8_T, MPI_UINT16_T, MPI_UINT32_T, MPI_UINT64_T
static final long MPI_JNULL, MPI_JBYTE, MPI_JDOUBLE, MPI_JBOOLEAN
static final long MPI_JCHAR, MPI_JSHORT, MPI_JINT, MPI_JLONG, MPI_JFLOAT
static final int MPI_THREAD_SINGLE, MPI_THREAD_FUNNELED, MPI_THREAD_SERIALIZED, MPI_THREAD_MULTIPLE
static final int MPI_PROC_NULL, MPI_ANY_SOURCE, MPI_ROOT
static final int MPI_ANY_TAG, MPI_UNDEFINED

// === 生命周期 ===
native static String MPI_Get_library_version() throws MPIException
native static void MPI_Init(String[] aArgs) throws MPIException
native static boolean MPI_Initialized() throws MPIException
native static int MPI_Comm_rank(long aComm) throws MPIException
native static int MPI_Comm_size(long aComm) throws MPIException
native static void MPI_Finalize() throws MPIException
native static boolean MPI_Finalized() throws MPIException
native static int MPI_Init_thread(String[] aArgs, int aRequired) throws MPIException

// === 通信器 ===
native static long MPI_Comm_create(long aComm, long aGroup) throws MPIException
native static long MPI_Comm_dup(long aComm) throws MPIException
native static void MPI_Comm_free(long aComm) throws MPIException
native static long MPI_Comm_split(long aComm, int aColor, int aKey) throws MPIException

// === 进程组 ===
native static long MPI_Comm_group(long aComm) throws MPIException
native static long MPI_Group_difference(long aGroup1, long aGroup2) throws MPIException
native static long MPI_Group_excl(long aGroup, int aN, int[] aRanks) throws MPIException
native static void MPI_Group_free(long aGroup) throws MPIException
native static long MPI_Group_incl(long aGroup, int aN, int[] aRanks) throws MPIException
native static long MPI_Group_intersection(long aGroup1, long aGroup2) throws MPIException
native static int MPI_Group_rank(long aGroup) throws MPIException
native static int MPI_Group_size(long aGroup) throws MPIException
native static long MPI_Group_union(long aGroup1, long aGroup2) throws MPIException

// === Barrier ===
native static void MPI_Barrier(long aComm) throws MPIException

// === 集合通信 (重载模式与 Comm 对应, Op→long, Datatype→long, Comm→long) ===
// MPI_Allgather / MPI_Allgatherv / MPI_Allreduce / MPI_Bcast
// MPI_Gather / MPI_Gatherv / MPI_Reduce / MPI_Scatter / MPI_Scatterv
native static byte MPI_AllreduceB(byte aB, long aOp, long aComm) throws MPIException
native static double MPI_AllreduceD(double aD, long aOp, long aComm) throws MPIException
native static boolean MPI_AllreduceZ(boolean aZ, long aOp, long aComm) throws MPIException
native static char MPI_AllreduceC(char aC, long aOp, long aComm) throws MPIException
native static short MPI_AllreduceS(short aS, long aOp, long aComm) throws MPIException
native static int MPI_AllreduceI(int aI, long aOp, long aComm) throws MPIException
native static long MPI_AllreduceL(long aL, long aOp, long aComm) throws MPIException
native static float MPI_AllreduceF(float aF, long aOp, long aComm) throws MPIException
// 同理: MPI_BcastB/D/Z/C/S/I/L/F, MPI_ReduceB/D/Z/C/S/I/L/F (多 int aRoot 参数)

// === 点对点 (重载模式与 Comm 对应) ===
native static void MPI_SendB(byte aB, int aDest, int aTag, long aComm) throws MPIException
native static void MPI_SendD(double aD, int aDest, int aTag, long aComm) throws MPIException
native static void MPI_SendZ(boolean aZ, int aDest, int aTag, long aComm) throws MPIException
native static void MPI_SendC(char aC, int aDest, int aTag, long aComm) throws MPIException
native static void MPI_SendS(short aS, int aDest, int aTag, long aComm) throws MPIException
native static void MPI_SendI(int aI, int aDest, int aTag, long aComm) throws MPIException
native static void MPI_SendL(long aL, int aDest, int aTag, long aComm) throws MPIException
native static void MPI_SendF(float aF, int aDest, int aTag, long aComm) throws MPIException
// MPI_RecvB/D/Z/C/S/I/L/F (有返回值)
// Sendrecv: 64 种数组类型组合 + 10 种 CPointer 组合
```
