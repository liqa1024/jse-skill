# ILogicalVectorOperation

> `jse.math.vector.ILogicalVectorOperation`

**核心职能**：任意的逻辑向量运算，包括与或非运算、填充遍历、统计、累积运算。

```java
// === 逻辑运算 (向量) ===
ILogicalVector and(ILogicalVector aRHS)
ILogicalVector or(ILogicalVector aRHS)
ILogicalVector xor(ILogicalVector aRHS)
ILogicalVector operate(ILogicalVector aRHS, IBooleanBinaryOperator aOpt)

// === 逻辑运算 (标量) ===
ILogicalVector and(boolean aRHS)
ILogicalVector or(boolean aRHS)
ILogicalVector xor(boolean aRHS)
ILogicalVector map(IBooleanUnaryOperator aOpt)

// === 原地运算 (向量) ===
void and2this(ILogicalVector aRHS)
void or2this(ILogicalVector aRHS)
void xor2this(ILogicalVector aRHS)
void operate2this(ILogicalVector aRHS, IBooleanBinaryOperator aOpt)

// === 原地运算 (标量) ===
void and2this(boolean aRHS)
void or2this(boolean aRHS)
void xor2this(boolean aRHS)
void map2this(IBooleanUnaryOperator aRHS)

// === 取反 ===
ILogicalVector not()
void not2this()

// === 填充与遍历 ===
void fill(boolean aRHS)
void fill(ILogicalVector aRHS)
void fill(ILogicalVectorGetter aRHS)
void assign(BooleanSupplier aSup)
void forEach(IBooleanConsumer aCon)

// === 统计 ===
boolean all()
boolean any()
int count()

// === 累积运算 ===
ILogicalVector cumall()
ILogicalVector cumany()
IVector cumcount()

// === 反转 ===
ILogicalVector reverse()
ILogicalVector refReverse()
void reverse2this()
@VisibleForTesting
default ILogicalVector refreverse()
```
