# RefLogicalVector

> `jse.math.vector.RefLogicalVector`

**核心职能**：`abstract class extends AbstractLogicalVector`。boolean 类型（逻辑）向量的引用视图基类。子类只需实现 `get()` 和 `size()`；`set()` 默认抛出 `UnsupportedOperationException("set")`，适用于不可变/只读向量视图。`newZeros_()` 委托给 `LogicalVector.zeros()`。

```java
// === 子类需实现 ===
abstract boolean get(int aIdx)
abstract int size()

// === 默认行为 ===
void set(int aIdx, boolean aValue)       // throws UnsupportedOperationException
boolean getAndSet(int aIdx, boolean aValue) // get + set 组合
```
