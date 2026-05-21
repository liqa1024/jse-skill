# IObjectPool

> `jse.cache.IObjectPool`

**核心职能**：定义线程安全的通用对象池接口，规范对象借用(`getObject`)与归还(`returnObject`)行为。所有缓存池均实现此接口。无基底接口，通过 `ObjectCachePool<T>` 或 `ThreadLocalObjectCachePool<T>` 实现。

```java
// === IObjectPool<T> ===
T getObject()                              // 借用对象（可能返回 null）
void returnObject(@NotNull T aObject)      // 归还对象
```
