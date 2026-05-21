# RefLongVector

> `jse.math.vector.RefLongVector`

**核心职能**：`abstract class extends AbstractLongVector`。long 类型向量的引用视图基类。子类只需实现 `get()` 和 `size()`；`set()` 默认抛出 `UnsupportedOperationException("set")`，适用于不可变/只读向量视图。`newZeros_()` 委托给 `LongVector.zeros()`。

```java
// === 子类需实现 ===
abstract long get(int aIdx)
abstract int size()

// === 默认行为 ===
void set(int aIdx, long aValue)      // throws UnsupportedOperationException
long getAndSet(int aIdx, long aValue) // get + set 组合
```
