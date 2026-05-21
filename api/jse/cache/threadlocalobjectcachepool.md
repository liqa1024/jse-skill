# ThreadLocalObjectCachePool\<T\>

> `jse.cache.ThreadLocalObjectCachePool`

**核心职能**：`implements IObjectPool<T>`。借助 `ThreadLocal<Deque<SoftReference<T>>>` 为每个线程维护独立缓存，实现高性能多线程并发访问同一实例。其余特性与 `ObjectCachePool` 一致：SoftReference 自动回收、不限制容量、不检测重复归还、受 `Conf.NO_CACHE` 控制。**重要**: 归还线程与借用线程必须一致。`new ThreadLocalObjectCachePool<>()` / `ThreadLocalObjectCachePool.withInitial(supplier)`。

```java
ThreadLocalObjectCachePool()
static <S> ThreadLocalObjectCachePool<S> withInitial(Supplier<? extends S> aSupplier)

protected T initialValue()

T getObject()
void returnObject(@NotNull T aObject)
```
