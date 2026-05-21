# AbstractFloatVectorOperation

> `jse.math.vector.AbstractFloatVectorOperation`

**核心职能**：`implements IFloatVectorOperation`。float 向量运算的骨架实现，仅提供填充/赋值/遍历和 reverse 操作。子类只需实现 2 个抽象方法。

```java
// === 抽象方法（子类须实现） ===
protected abstract IFloatVector thisVector_()
protected abstract IFloatVector newVector_(int aSize)

// === 填充 / 赋值 / 遍历 ===
void fill(float aRHS)
void fill(IFloatVector aRHS)
void fill(IFloatVectorGetter aRHS)
void assign(IFloatSupplier aSup)
void forEach(IFloatConsumer aCon)

// === 向量额外运算 ===
IFloatVector reverse()
IFloatVector refReverse()
void reverse2this()
```
