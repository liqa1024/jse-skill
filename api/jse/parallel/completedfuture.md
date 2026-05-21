# CompletedFuture\<T\>

> `jse.parallel.CompletedFuture`

**核心职能**：`final class implements Future<T>`。包装一个已就绪值，用于在未提交任务即退出的方法中返回非 null 的 Future。`isDone()` 恒为 `true`，`cancel()` 恒为 `false`。

```java
CompletedFuture(T aOut)
boolean cancel(boolean mayInterruptIfRunning)
boolean isCancelled()
boolean isDone()
T get()
T get(long timeout, TimeUnit unit)
```
