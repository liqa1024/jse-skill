# MergedFuture\<T, F\>

> `jse.parallel.MergedFuture`

**核心职能**：`implements Future<List<T>>`。将 `Iterable<F extends Future<? extends T>>` 合并为单个 `Future<List<T>>`，`get()` 按迭代顺序收集。超时版将剩余时间依次分配，耗尽即抛 `TimeoutException`。

```java
MergedFuture(Iterable<F> aFutures)
boolean cancel(boolean mayInterruptIfRunning)
boolean isCancelled()
boolean isDone()
List<T> get() throws InterruptedException, ExecutionException
List<T> get(long timeout, TimeUnit unit) throws InterruptedException, ExecutionException, TimeoutException
```
