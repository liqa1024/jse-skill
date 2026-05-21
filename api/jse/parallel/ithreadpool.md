# IThreadPool

> `jse.parallel.IThreadPool`

**核心职能**：顶层线程池管理接口，继承 `AutoCloseable` 支持 try-with-resources 自动关闭。`close()` 默认实现为 `shutdown()` + `awaitTermination()`，忽略 `InterruptedException` 以保证后续资源正常释放。

```java
void shutdown()
void shutdownNow()
boolean isShutdown()
boolean isTerminated()
void awaitTermination() throws InterruptedException

void waitUntilDone() throws InterruptedException
int njobs()
int nthreads()

// === AutoCloseable ===
default void close() throws Exception    // shutdown() + awaitTermination()
```
