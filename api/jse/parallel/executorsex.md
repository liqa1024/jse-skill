# ExecutorsEX

> `jse.parallel.ExecutorsEX`

**核心职能**：类似 `java.util.concurrent.Executors` 的工具类。`newFixedThreadPool(int)` 创建固定大小线程池（带 `allowCoreThreadTimeOut`）。预置 `SERIAL_EXECUTOR` 串行执行器——直接在当前线程运行，不可关闭，可复用。

```java
static IExecutorEX newFixedThreadPool(int nThreads)
static final IExecutorEX SERIAL_EXECUTOR
```
