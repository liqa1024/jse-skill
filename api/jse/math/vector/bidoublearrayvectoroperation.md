# BiDoubleArrayVectorOperation

> `jse.math.vector.BiDoubleArrayVectorOperation`

**核心职能**：`extends AbstractComplexVectorOperation`。复类型向量的 ARRAY/DATA 双路径运算实现，使用 `double[2][]` 交错存储。优先尝试直接操作底层数组（ARRAY 路径），不兼容时回退至接口调用（DATA 路径）。目前只优化相同类型的向量之间的运算。

```java
// === 算术运算 (IComplexVector) ===
IComplexVector plus(IComplexVector aRHS)
IComplexVector minus(IComplexVector aRHS)
IComplexVector lminus(IComplexVector aRHS)
IComplexVector multiply(IComplexVector aRHS)
IComplexVector div(IComplexVector aRHS)
IComplexVector ldiv(IComplexVector aRHS)
IComplexVector operate(IComplexVector aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 算术运算 (IComplexDouble) ===
IComplexVector plus(IComplexDouble aRHS)
IComplexVector minus(IComplexDouble aRHS)
IComplexVector lminus(IComplexDouble aRHS)
IComplexVector multiply(IComplexDouble aRHS)
IComplexVector div(IComplexDouble aRHS)
IComplexVector ldiv(IComplexDouble aRHS)

// === 算术运算 (标量 double) ===
IComplexVector plus(double aRHS)
IComplexVector minus(double aRHS)
IComplexVector lminus(double aRHS)
IComplexVector multiply(double aRHS)
IComplexVector div(double aRHS)
IComplexVector ldiv(double aRHS)
IComplexVector map(IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)

// === 原地运算 (IComplexVector) ===
void plus2this(IComplexVector aRHS)
void minus2this(IComplexVector aRHS)
void lminus2this(IComplexVector aRHS)
void multiply2this(IComplexVector aRHS)
void div2this(IComplexVector aRHS)
void ldiv2this(IComplexVector aRHS)
void operate2this(IComplexVector aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 原地运算 (IComplexDouble) ===
void plus2this(IComplexDouble aRHS)
void minus2this(IComplexDouble aRHS)
void lminus2this(IComplexDouble aRHS)
void multiply2this(IComplexDouble aRHS)
void div2this(IComplexDouble aRHS)
void ldiv2this(IComplexDouble aRHS)

// === 原地运算 (标量 double) ===
void plus2this(double aRHS)
void minus2this(double aRHS)
void lminus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)
void ldiv2this(double aRHS)
void map2this(IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)

// === 取反 ===
IComplexVector negative()
void negative2this()

// === 填充与遍历 ===
void fill(IComplexDouble aRHS)
void fill(double aRHS)
void fill(IComplexVector aRHS)
void fill(IComplexVectorGetter aRHS)
void fill(IVectorGetter aRHS)
void assign(Supplier<? extends IComplexDouble> aSup)
void assign(DoubleSupplier aSup)
void forEach(Consumer<? super ComplexDouble> aCon)
void forEach(IDoubleBinaryConsumer aCon)

// --- Groovy 闭包支持 ---
void fill(@ClosureParams(value=SimpleType.class, options="int") Closure<?> aRHS)
void assign(Closure<?> aSup)

// === 统计 ===
ComplexDouble sum()
ComplexDouble mean()
ComplexDouble prod()
ComplexDouble stat(IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 点积 ===
ComplexDouble dot(IComplexVector aRHS)
double dot()

// === 反转 ===
IComplexVector reverse()

// === 复合运算 ===
void mplus2this(IComplexVector aRHS, double aMul)
void mplus2this(IComplexVector aRHS, IComplexDouble aMul)

// === 子类需实现 ===
protected abstract BiDoubleArrayVector thisVector_()
protected abstract BiDoubleArrayVector newVector_(int aSize)
```
