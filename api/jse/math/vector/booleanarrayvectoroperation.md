# BooleanArrayVectorOperation

> `jse.math.vector.BooleanArrayVectorOperation`

**核心职能**：`extends AbstractLogicalVectorOperation`。boolean 类型（逻辑）向量的 ARRAY/DATA 双路径运算实现。优先尝试直接操作 `boolean[]` 底层数组（ARRAY 路径），不兼容时回退至接口调用（DATA 路径）。

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
void map2this(IBooleanUnaryOperator aOpt)

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

// === 反转 ===
ILogicalVector reverse()

// === 子类需实现 ===
protected abstract BooleanArrayVector thisVector_()
protected abstract BooleanArrayVector newVector_(int aSize)
```
