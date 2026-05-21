# FloatArrayVectorOperation

> `jse.math.vector.FloatArrayVectorOperation`

**核心职能**：`abstract class extends AbstractFloatVectorOperation`。面向 `FloatArrayVector` 的运算优化层，ARRAY/DATA 双路径覆盖填充、赋值、遍历及反转操作。

```java
// === 填充 / 赋值 / 遍历 ===
void fill(float)
void fill(IFloatVector)
void fill(IFloatVectorGetter)
void assign(IFloatSupplier)
void forEach(IFloatConsumer)

// === 向量额外 ===
IFloatVector reverse()

// === 子类需实现 ===
protected abstract FloatArrayVector thisVector_()
protected abstract FloatArrayVector newVector_(int aSize)
```
