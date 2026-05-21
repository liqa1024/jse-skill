# ISetOnlyIterator / ISetIterator

> `jse.code.iterator.ISetOnlyIterator` / `jse.code.iterator.ISetIterator`

**核心职能**：定义泛型设置(set-only)和读写(read-write)迭代器协议，作为基本类型迭代器的泛型对应。接口，不由 Groovy 直接实例化。

```java
// ISetOnlyIterator<E> — 仅设置
boolean hasNext()
void nextOnly()
void set(E e)
default void nextAndSet(E e)

// ISetIterator<E> — 读写（extends Iterator<E>, ISetOnlyIterator<E>）
// 继承 Iterator<E> 的全部方法 + ISetOnlyIterator<E> 的全部方法
```
