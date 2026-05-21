# AbstractLogicalVectorOperation

> `jse.math.vector.AbstractLogicalVectorOperation`

**核心职能**：逻辑型向量的运算骨架，实现 `ILogicalVectorOperation`。提供逻辑运算（and/or/xor/not）、填充/赋值/遍历、all/any/count、累积运算（cumall/cumany/cumcount）、反向等操作的默认实现。继承需实现 `thisVector_`/`newVector_`。

```java
// === 逻辑运算：向量-向量 ===
ILogicalVector and(ILogicalVector aRHS)
ILogicalVector or(ILogicalVector aRHS)
ILogicalVector xor(ILogicalVector aRHS)
ILogicalVector operate(ILogicalVector aRHS, IBooleanBinaryOperator aOpt)
void and2this(ILogicalVector aRHS)
void or2this(ILogicalVector aRHS)
void xor2this(ILogicalVector aRHS)
void operate2this(ILogicalVector aRHS, IBooleanBinaryOperator aOpt)

// === 逻辑运算：标量 ===
ILogicalVector and(boolean aRHS)
ILogicalVector or(boolean aRHS)
ILogicalVector xor(boolean aRHS)
ILogicalVector map(IBooleanUnaryOperator aOpt)
void and2this(boolean aRHS)
void or2this(boolean aRHS)
void xor2this(boolean aRHS)
void map2this(IBooleanUnaryOperator aOpt)

// === 非运算 ===
ILogicalVector not()
void not2this()

// === 填充/赋值/遍历 ===
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

// === 反向 ===
ILogicalVector reverse()
ILogicalVector refReverse()
void reverse2this()

// === 子类需实现 ===
protected abstract ILogicalVector thisVector_()
protected abstract ILogicalVector newVector_(int aSize)
protected IVector newRealVector_(int aSize)
```
