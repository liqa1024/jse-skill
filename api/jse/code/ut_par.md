# UT.Par

> `jse.code.UT.Par`

**核心职能**：并行工具集——SplittableRandom 随机数拆分、Future 组合与转换、流重定向，以及面向 Groovy Closure 的 parfor/parwhile 并行循环。

```java
// 按需拆分随机数生成器（基于 SplittableRandom，多线程安全）
static IRandom[] splitRandoms(int aSize, long aSeed)
static IRandom[] splitRandoms(int aSize)
static IRandom splitRandom(MPI.Comm aComm, long aSeed) throws MPIException
static IRandom splitRandom(MPI.Comm aComm) throws MPIException

// 获取/创建全局 ParforThreadPool
static @NotNull ParforThreadPool pool(@Range int aThreadNum)

// Future 操作
static <T> Future<List<T>> mergeAll(Iterable<? extends Future<? extends T>> aFutures)
static <R, T> Future<R> map(Future<T> aFuture, IUnaryFullOperator<? extends R, ? super T> aOpt)
static <U> Future<U> callAsync(Callable<U> aCallable)
static <U> Future<U> supplyAsync(Supplier<U> aSupplier)
static Future<Void> runAsync(Runnable aRunnable)

// 流重定向（异步）
static Future<Void> redirectStream(InputStream aFrom, boolean aAutoCloseFrom, OutputStream aTo, boolean aAutoCloseTo)
static Future<Void> redirectStream(InputStream aFrom, boolean aAutoCloseFrom, OutputStream aTo)
static Future<Void> redirectStream(InputStream aFrom, OutputStream aTo, boolean aAutoCloseTo)
static Future<Void> redirectStream(InputStream aFrom, OutputStream aTo)

// parfor/parwhile（Groovy Closure 版本）
@VisibleForTesting static void parfor(int aSize, Closure<?> aGroovyTask)           // :note: Groovy 脚本优先使用 parfor(Closure) 闭包重载
@VisibleForTesting static void parfor(int aSize, int aThreadNum, Closure<?> aGroovyTask)  // :note: Groovy 脚本优先使用 parfor(Closure) 闭包重载
@VisibleForTesting static void parwhile(ParforThreadPool.IParwhileChecker aChecker, Closure<?> aGroovyTask)    // :note: Groovy 脚本优先使用 parwhile(Closure) 闭包重载
@VisibleForTesting static void parwhile(ParforThreadPool.IParwhileChecker aChecker, int aThreadNum, Closure<?> aGroovyTask)  // :note: Groovy 脚本优先使用 parwhile(Closure) 闭包重载
```
