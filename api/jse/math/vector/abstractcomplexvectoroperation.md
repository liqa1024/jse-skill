# AbstractComplexVectorOperation

> `jse.math.vector.AbstractComplexVectorOperation`

**核心职能**：复数向量的运算骨架，实现 `IComplexVectorOperation`。提供算术运算（plus/minus/multiply/div/lminus/ldiv，支持 `IComplexVector`/`IVector`/`IComplexDouble`/`double` 四种 RHS）、FMA（mplus2this）、统计（sum/mean/prod）、累积运算（cumsum/cummean/cumprod/cumstat）、点积/模/绝对值、反向等操作的默认实现。继承需实现 `thisVector_`/`newVector_`。

```java
// === 算术运算：IComplexVector RHS ===
IComplexVector plus(IComplexVector aRHS)
IComplexVector minus(IComplexVector aRHS)
IComplexVector lminus(IComplexVector aRHS)
IComplexVector multiply(IComplexVector aRHS)
IComplexVector div(IComplexVector aRHS)
IComplexVector ldiv(IComplexVector aRHS)
IComplexVector operate(IComplexVector aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)
void plus2this(IComplexVector aRHS)
void minus2this(IComplexVector aRHS)
void lminus2this(IComplexVector aRHS)
void multiply2this(IComplexVector aRHS)
void div2this(IComplexVector aRHS)
void ldiv2this(IComplexVector aRHS)
void operate2this(IComplexVector aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 算术运算：IVector RHS ===
IComplexVector plus(IVector aRHS)
IComplexVector minus(IVector aRHS)
IComplexVector lminus(IVector aRHS)
IComplexVector multiply(IVector aRHS)
IComplexVector div(IVector aRHS)
IComplexVector ldiv(IVector aRHS)
IComplexVector operate(IVector aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, Double> aOpt)
void plus2this(IVector aRHS)
void minus2this(IVector aRHS)
void lminus2this(IVector aRHS)
void multiply2this(IVector aRHS)
void div2this(IVector aRHS)
void ldiv2this(IVector aRHS)
void operate2this(IVector aRHS, IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, Double> aOpt)

// === 算术运算：IComplexDouble RHS ===
IComplexVector plus(IComplexDouble aRHS)
IComplexVector minus(IComplexDouble aRHS)
IComplexVector lminus(IComplexDouble aRHS)
IComplexVector multiply(IComplexDouble aRHS)
IComplexVector div(IComplexDouble aRHS)
IComplexVector ldiv(IComplexDouble aRHS)
void plus2this(IComplexDouble aRHS)
void minus2this(IComplexDouble aRHS)
void lminus2this(IComplexDouble aRHS)
void multiply2this(IComplexDouble aRHS)
void div2this(IComplexDouble aRHS)
void ldiv2this(IComplexDouble aRHS)

// === 算术运算：double RHS ===
IComplexVector plus(double aRHS)
IComplexVector minus(double aRHS)
IComplexVector lminus(double aRHS)
IComplexVector multiply(double aRHS)
IComplexVector div(double aRHS)
IComplexVector ldiv(double aRHS)
void plus2this(double aRHS)
void minus2this(double aRHS)
void lminus2this(double aRHS)
void multiply2this(double aRHS)
void div2this(double aRHS)
void ldiv2this(double aRHS)

// === 一元运算 ===
IComplexVector map(IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
void map2this(IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
IComplexVector negative()
void negative2this()

// === 填充/赋值/遍历 ===
void fill(IComplexDouble aRHS)
void fill(double aRHS)
void fill(IComplexVector aRHS)
void fill(IVector aRHS)
void fill(IComplexVectorGetter aRHS)
void fill(IVectorGetter aRHS)
void assign(Supplier<? extends IComplexDouble> aSup)
void assign(DoubleSupplier aSup)
void forEach(Consumer<? super ComplexDouble> aCon)
void forEach(IDoubleBinaryConsumer aCon)
// Groovy Closure overloads
void fill(@ClosureParams(value=SimpleType.class, options="int") Closure<?> aGroovyTask)
void assign(Closure<?> aGroovyTask)
void forEach(@ClosureParams(value=FromString.class, options={"ComplexDouble", "double,double"}) Closure<?> aGroovyTask)

// === 统计 ===
ComplexDouble sum()
ComplexDouble mean()
ComplexDouble prod()
ComplexDouble stat(IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 累积运算 ===
IComplexVector cumsum()
IComplexVector cummean()
IComplexVector cumprod()
IComplexVector cumstat(IBinaryFullOperator<? extends IComplexDouble, ? super ComplexDouble, ? super ComplexDouble> aOpt)

// === 点积/模/绝对值 ===
ComplexDouble dot(IComplexVector aRHS)
ComplexDouble dot(IVector aRHS)
double dot()
double norm()
IVector abs()

// === 反向 ===
IComplexVector reverse()
IComplexVector refReverse()
void reverse2this()

// === FMA ===
void mplus2this(IComplexVector aRHS, double aMul)
void mplus2this(IComplexVector aRHS, IComplexDouble aMul)

// === 子类需实现 ===
protected abstract IComplexVector thisVector_()
protected abstract IComplexVector newVector_(int aSize)
protected IVector newRealVector_(int aSize)
```
