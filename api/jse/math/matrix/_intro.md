# `jse.math.matrix`

> 41 个文件，4 种数据类型（double/complex/int/boolean），统一分层架构。**`Matrices` 为工厂入口**，独立于类型继承体系。

## 架构总览 (Architecture)

4 种类型共享同一分层模式。以 double 为例：`IMatrix`（接口）→ `AbstractMatrix`（骨架）→ `DoubleArrayMatrix`（`IDataShell<double[]>` 数组层）→ `ColumnMatrix`/`RowMatrix`（列/行主序实现，`mShift` 零拷贝切片）。

```
I{Type}Matrix (接口)      I{Type}MatrixOperation (运算)     I{Type}MatrixSlicer (2D切片)
    ↑                              ↑                              ↑
Abstract{Type}Matrix         Abstract{Type}MatrixOperation      Abstract{Type}MatrixSlicer
    ↑                              ↑
{Type}ArrayMatrix (IDataShell)     {Type}ArrayMatrixOperation (ARRAY 优化)
    ↑
Column{Type}Matrix / Row{Type}Matrix (列/行主序)    Ref{Type}Matrix (引用视图)
```

**跨类型对比**

| 特性 | double | complex | int | logical |
|---|---|---|---|---|
| **算术运算符** | plus/minus/multiply/div/mod (含 l*) | plus/minus/multiply/div + lminus/ldiv (标量+矩阵) | ❌ | ❌ |
| **矩阵乘法** | matmul/lmatmul + 2this/2dest | ❌ | ❌ | ❌ |
| **行列统计** | sumOfCols/Rows, meanOfCols/Rows | ❌ | ❌ | ❌ |
| **转置** | transpose/refTranspose (Column↔Row 零拷贝) | transpose/refTranspose | transpose/refTranspose | transpose/refTranspose |
| **跨类型转换** | asVecCol/Row → IVector | real/imag → IMatrix | asMat → IMatrix | asMat→IMatrix, asIntMat→IIntMatrix |
| **numpy** | NDArray<double[]> (shift=0 零拷贝) | ❌ | NDArray<int[]> | NDArray<boolean[]> |
| **Groovy 运算符** | + - * / % (标量+矩阵) | + - * / (标量+矩阵) | ❌ | ❌ |
| **内部存储** | double[] | double[2][] | int[] | boolean[] |
| **数组优化类** | DoubleArrayMatrixOp | BiDoubleArrayMatrixOp | IntArrayMatrixOp | BooleanArrayMatrixOp |
