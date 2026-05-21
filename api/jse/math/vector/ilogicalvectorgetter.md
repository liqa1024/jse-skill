# ILogicalVectorGetter

> `jse.math.vector.ILogicalVectorGetter`

**核心职能**：函数式接口，获取 boolean 向量元素值。继承 `IIndexFilter` 避免 lambda 重载冲突。

```java
@FunctionalInterface
boolean get(int aIdx)
@VisibleForTesting
default boolean accept(int aIdx)
```
