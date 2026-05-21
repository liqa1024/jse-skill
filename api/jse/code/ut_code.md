# UT.Code

> `jse.code.UT.Code`

**核心职能**：通用代码辅助方法集——随机种子/ID（含 MPI 广播）与唯一 ID 为外部常用；null 安全类型转换、Groovy 集合操作封装与 Map 键值查找为内部使用。

```java
// 打印带栈信息的警告（DEBUG 模式下包含 jse 内核栈）
static void warning(String aMsg)
static void printStackTrace(Throwable t)

// null 安全的类型转换
@Contract("null->null; !null->!null")
static @Nullable String toString(@Nullable Object aObj)
static double doubleValue(@Nullable Number aNumber)    // null 返回 NaN
static float floatValue(@Nullable Number aNumber)      // null 返回 NaN

// 随机种子（用于 LAMMPS），范围 [1, MAX_SEED]
static int randSeed()
static int randSeed(long aSeed)
static int randSeed(IRandom aRng)
static int randSeed(MPI.Comm aComm, int aRoot) throws MPIException
static int randSeed(MPI.Comm aComm, int aRoot, long aSeed) throws MPIException
static int randSeed(MPI.Comm aComm, int aRoot, IRandom aRng) throws MPIException

// 随机 ID（≤16 位十六进制字符串）
static String randID()
static String randID(long aSeed)
static String randID(IRandom aRng)
static String randID(MPI.Comm aComm, int aRoot) throws MPIException
static String randID(MPI.Comm aComm, int aRoot, long aSeed) throws MPIException
static String randID(MPI.Comm aComm, int aRoot, IRandom aRng) throws MPIException

// 唯一 ID（16 位十六进制，基于对象内容的深度哈希）
static String uniqueID(Object... aObjects)

// 按顺序从 Map 中获取第一个存在的键值
static Object get(Map<?, ?> aMap, Object... aKeys)
static Object getWithDefault(Map<?, ?> aMap, Object aDefaultValue, Object... aKeys)

// :note: Groovy 集合方法包装（内部使用，Groovy 脚本中优先使用原生语法糖）
static <T> T removeLast(List<T> self)
static <T> T last(Iterable<T>/List<T>/Deque<T>/T[] self)
static <T> T first(Iterable<T>/List<T>/T[] self)
static <T> T max/min(Iterable<T>/T[] self)
static <T> Object sum(Iterable<T>/Object[] self)
static boolean contains(Object[]/int[] self, Object aValue)

// 类型优化转换
static ComplexDouble toComplexDouble(IComplexDouble aComplexDouble)
@VisibleForTesting static XYZ toXYZ(IXYZ aXYZ)

// 集合合并（T[]+T[], List+List, Iterable+Iterable, 嵌套展平等 18 个重载）
@VisibleForTesting static <T> List<T>/Iterable<T> merge(...)

// 集合过滤
@VisibleForTesting static <T> Iterable<T> filter(Iterable<T>, IFilter<T>)
@VisibleForTesting static Iterable<Integer> filterInt(Iterable<Integer>/IHasIntIterator/int, IIndexFilter)
@VisibleForTesting static Iterable<? extends Number>/IHasDoubleIterator filterDouble(Iterable/IHasDoubleIterator, IDoubleFilter)

// 集合映射
@VisibleForTesting static <R,T> Iterable/R>/Iterator<R>/Collection<R>/List<R> map(Iterable/Iterator/Collection/List/T[], IUnaryFullOperator)

// 数组转 List / 整数范围
@VisibleForTesting static List<Double>/List<Integer>/List<Boolean> asList(double[]/int[]/boolean[])
@VisibleForTesting static List<Integer> range_(int size/start/start,stop/start,stop,step) // 闭区间
@VisibleForTesting static List<Integer> range(int size/start/start,stop/start,stop,step)  // 开区间
```
