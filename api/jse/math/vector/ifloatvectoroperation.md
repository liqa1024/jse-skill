# IFloatVectorOperation

> `jse.math.vector.IFloatVectorOperation`

**核心职能**：任意的单精度向量运算。

```java
// === 填充与遍历 ===
void fill(float aRHS)
void fill(IFloatVector aRHS)
void fill(IFloatVectorGetter aRHS)
void assign(IFloatSupplier aSup)
void forEach(IFloatConsumer aCon)

// === 向量额外运算 ===
IFloatVector reverse()
IFloatVector refReverse()
void reverse2this()
@VisibleForTesting
default IFloatVector refreverse()
```
