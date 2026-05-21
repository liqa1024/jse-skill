# RefIntVector

> `jse.math.vector.RefIntVector`

**核心职能**：`abstract class extends AbstractIntVector`。一般 int 向量的默认实现基类，`newZeros_()` 委托给 `IntVector.zeros()`。只读设计 — `set()` 默认抛 `UnsupportedOperationException`。

```java
// === 构造 ===
protected final IIntVector newZeros_(int aSize)

// === 只读接口 ===
abstract int get(int aIdx)
void set(int aIdx, int aValue)              // throws UnsupportedOperationException
int getAndSet(int aIdx, int aValue)

// === 尺寸 ===
abstract int size()
```
