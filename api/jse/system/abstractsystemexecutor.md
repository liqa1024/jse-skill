# AbstractSystemExecutor

> `jse.system.AbstractSystemExecutor`

**核心职能**：`implements ISystemExecutor`。实现全部 `system`/`submitSystem` 变体的统一包装——`system`=同步等待 Future、`submitSystem_str` 返回包装后的 `Future<List<String>>`。内置 `mDead` 标志 + `mRunningSystem` 任务追踪，`shutdown()` 异步等待完成后清理。`IDoFinalFuture` 内部接口支持任务完成回调。

```java
// 子类可覆写
protected long sleepTime() → SYNC_SLEEP_TIME_2        // 轮询间隔
protected void shutdownFinal()                         // shutdown 完成回调

// 抽象方法 (子类实现)
abstract Future<Integer> submitSystem__(String aCommand, IWriteln aWriteln)
abstract void putFiles_(Iterable<String> aFiles) throws Exception
abstract void getFiles_(Iterable<String> aFiles) throws Exception
```
