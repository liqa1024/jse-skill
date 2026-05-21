# RefFloatVector

> `jse.math.vector.RefFloatVector`

**核心职能**：`abstract class extends AbstractFloatVector`。一般 float 向量的默认实现基类，`newZeros_()` 委托给 `FloatVector.zeros()`。只读设计 — `set()` 默认抛 `UnsupportedOperationException`。

```java
// === 构造 ===
protected final IFloatVector newZeros_(int aSize)

// === 只读接口 ===
abstract float get(int aIdx)
void set(int aIdx, float aValue)            // throws UnsupportedOperationException
float getAndSet(int aIdx, float aValue)

// === 尺寸 ===
abstract int size()
```
