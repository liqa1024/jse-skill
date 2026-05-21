# RefVector

> `jse.math.vector.RefVector`

**核心职能**：`abstract class extends AbstractVector`。一般向量的默认实现基类，`newZeros_()` 委托给 `Vector.zeros()`。只读设计 — `set()` 默认抛 `UnsupportedOperationException`。

```java
// === 构造 ===
protected final IVector newZeros_(int aSize)

// === 只读接口 ===
abstract double get(int aIdx)
void set(int aIdx, double aValue)           // throws UnsupportedOperationException
double getAndSet(int aIdx, double aValue)

// === 尺寸 ===
abstract int size()
```
