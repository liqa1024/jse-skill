# ObjectCachePool

> `jse.cache.ObjectCachePool`

**核心职能**：`implements IObjectPool<T>`。基于 `SoftReference` + `ArrayDeque` 的通用对象池实现。GC 内存不足时自动释放缓存。**单线程不安全但不同实例间线程安全**。统一不设缓存数量上限，不检测重复归还。受 `Conf.NO_CACHE` 控制——开启时不缓存，每次 `getObject` 均调用 `initialValue()` 新建。`new ObjectCachePool<>()` / `ObjectCachePool.withInitial(supplier)`。

```java
ObjectCachePool()
static <S> ObjectCachePool<S> withInitial(Supplier<? extends S> aSupplier)

// 子类覆写此方法以提供默认构造逻辑（默认返回 null）
protected T initialValue()

T getObject()
void returnObject(@NotNull T aObject)
```
