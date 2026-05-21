# ParforThreadPool

> `jse.parallel.ParforThreadPool`

> 此类标记为 `@ApiStatus.Experimental`

**核心职能**：`final class implements IThreadPool`。类似 MATLAB `parfor` 语义的线程池。自动识别 `nthreads()<=1` 串行执行。`parfor` 支持非竞争模式（`mNoCompetitive`，各线程按 `threadID` 步长分配任务）与竞争模式（CAS 自旋抢任务）。`parwhile` 通过 `IParwhileChecker` 控制循环终止，仅竞争模式。内置 `CountDownLatch` 同步 + `AtomicReference<Exception>` 错误传播。每个线程独立 `ReentrantLock` 保证写入可见性。

```java
ParforThreadPool(int aNumThreads, boolean aNoCompetitive)
ParforThreadPool(int aNumThreads)

// === IThreadPool ===
void shutdown() / void shutdownNow()
boolean isShutdown() / boolean isTerminated()
int njobs() / int nthreads()
void awaitTermination() throws InterruptedException
void waitUntilDone() throws InterruptedException

// === parfor: 并行 for (i=0; i<aSize; ++i) ===
void parfor(int aSize, Runnable aTask)
void parfor(int aSize, IParforTask aTask)
void parfor(int aSize, IParforTaskWithID aTaskWithID)
void parfor(int aSize, ITaskWithID aInitDo, ITaskWithID aFinalDo, IParforTaskWithID aTaskWithID)
@ApiStatus.Experimental void parforWithException(int aSize, ITaskWithIDAndException aInitDo, ITaskWithIDAndException aFinalDo, IParforTaskWithIDAndException aTaskWithIDAndException) throws Exception

// === parwhile: 并行 while (aChecker.noBreak()) ===
void parwhile(IParwhileChecker aChecker, Runnable aTask)
void parwhile(IParwhileChecker aChecker, IParwhileTaskWithID aTaskWithID)
void parwhile(IParwhileChecker aChecker, ITaskWithID aInitDo, ITaskWithID aFinalDo, IParwhileTaskWithID aTaskWithID)

// === 函数式接口 ===
@FunctionalInterface interface ITaskWithID { void run(int threadID) }
@FunctionalInterface interface IParforTask { void run(int i) }
@FunctionalInterface interface IParforTaskWithID { void run(int i, int threadID) }
@FunctionalInterface interface ITaskWithIDAndException { void run(int threadID) throws Exception }
@FunctionalInterface interface IParforTaskWithIDAndException { void run(int i, int threadID) throws Exception }
@FunctionalInterface interface IParwhileChecker { boolean noBreak() }
@FunctionalInterface interface IParwhileTaskWithID { void run(int threadID) }
```
