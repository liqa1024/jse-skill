# IMatrixOperation

> `jse.math.matrix.IMatrixOperation`

**核心职能**：分离式运算接口。与 `IVectorOperation` 镜像但增加矩阵乘法 (`matmul`)、行列统计、转置。三种变体：返回新矩阵、2this 原地、2dest 写入目标。

```java
// === 向量-向量运算（返回新矩阵） ===
IMatrix plus/minus/lminus/multiply/div/ldiv/mod/lmod(IMatrix)
IMatrix operate(IMatrix, DoubleBinaryOperator)
void plus2this/minus2this/lminus2this/multiply2this/div2this/ldiv2this/mod2this/lmod2this(IMatrix)
void operate2this(IMatrix, DoubleBinaryOperator)
void plus2dest/minus2dest/.../lmod2dest(IMatrix, IMatrix rDest)

// === 标量运算 ===
IMatrix plus/minus/lminus/multiply/div/ldiv/mod/lmod(double)
IMatrix map(DoubleUnaryOperator)
void plus2this/.../lmod2this(double); void map2this(DoubleUnaryOperator)
void plus2dest/.../lmod2dest(double, IMatrix rDest); void map2dest(IMatrix rDest, DoubleUnaryOperator)

// === 一元 ===
IMatrix abs() / void abs2this(); IMatrix negative() / void negative2this()

// === 填充/赋值/遍历 ===
void fill(double/IMatrix/IMatrixGetter)
void assignCol(DoubleSupplier) / assignRow(DoubleSupplier)
void forEachCol(DoubleConsumer) / forEachRow(DoubleConsumer)

// === 统计 ===
double sum() / mean() / max() / min()

// === 矩阵乘法 ===
// :note: 实验性简单实现，效率不如 NumPy/BLAS，生产环境建议通过 NumPy 完成矩阵乘法
IMatrix matmul(IMatrix) / lmatmul(IMatrix)        // this × RHS / RHS × this
void matmul2this(IMatrix) / lmatmul2this(IMatrix)
void matmul2dest(IMatrix, IMatrix rDest) / lmatmul2dest(IMatrix, IMatrix rDest)

// === 行列统计 ===
IVector sumOfCols() / sumOfRows()                 // 每列/行求和
IVector meanOfCols() / meanOfRows()               // 每列/行均值

// === 转置 / 对角 ===
IMatrix transpose()                                // 新矩阵
IMatrix refTranspose()                             // 引用视图（Column↔Row 零拷贝）
boolean isDiag()                                   // 是否对角阵
```
