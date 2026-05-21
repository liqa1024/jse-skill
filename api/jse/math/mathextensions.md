# MathExtensions

> `jse.math.MathExtensions`

**核心职能**：为 Groovy 提供 `Number + IVector`, `IComplexDouble * IComplexMatrix` 等左侧运算（Groovy `@Extension` 风格）。全静态方法类。

```java
// Number/Integer + Vector (IVector/IIntVector/ILogicalVector)
static IVector plus/minus/multiply/div/mod(Number, IVector)
static IIntVector plus/minus/multiply/div/mod(Integer, IIntVector)
static ILogicalVector and/or/xor(Boolean, ILogicalVector)

// Number + Matrix
static IMatrix plus/minus/multiply/div/mod(Number, IMatrix)

// IComplexDouble/Number/IVector + ComplexVector
static IComplexVector plus/minus/multiply/div(IComplexDouble/Number/IVector, IComplexVector)

// IComplexDouble/Number/IMatrix + ComplexMatrix
static IComplexMatrix plus/minus/multiply/div(IComplexDouble/Number/IMatrix, IComplexMatrix)

// Number + IComplexDouble
static ComplexDouble plus/minus/multiply/div(Number, IComplexDouble)
```
