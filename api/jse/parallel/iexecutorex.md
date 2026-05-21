# IExecutorEX

> `jse.parallel.IExecutorEX`

**核心职能**：继承 `IThreadPool`，在标准 `ExecutorService` 接口之外增加 `waitUntilDone()`（轮询 `getActiveCount`+队列直到归零）、`njobs()`（活跃+排队任务总数）、`nthreads()` 三个扩展方法。

```java
// === ExecutorService 标准 ===
void execute(Runnable aRun)
Future<?> submit(Runnable aRun)
<T> Future<T> submit(Callable<T> aCall)
void shutdown()
void shutdownNow()
boolean isShutdown()
boolean isTerminated()
void awaitTermination() throws InterruptedException

// === 扩展 ===
void waitUntilDone() throws InterruptedException
int njobs()
int nthreads()
```
