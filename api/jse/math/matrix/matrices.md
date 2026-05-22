# Matrices

> `jse.math.matrix.Matrices`

**核心职能**：创建各类矩阵的统一静态工厂。默认返回 `RowMatrix`。涵盖 `ones/zeros/NaN`、从 `IMatrixGetter`/`Closure`/`Collection`/numpy 转换、`diag` 对角矩阵、布尔/整数矩阵构造。`final class`，私有构造函数，纯静态方法类。

```java
// === 默认 double 构造（返回 RowMatrix） ===
static RowMatrix zeros(int size) / zeros(int nRows, int nCols)
static RowMatrix ones(int size) / ones(int nRows, int nCols)
static RowMatrix NaN(int size) / NaN(int nRows, int nCols)

// === 从已有数据拷贝 ===
// :note: Groovy 中列表直接匹配 Collection/Iterable 重载
static RowMatrix from(int size, IMatrixGetter) / from(int nRows, int nCols, IMatrixGetter)
static RowMatrix from(IMatrix)                              // 复制为 RowMatrix
static RowMatrix from(Collection<?> rows) / fromRows(Collection) / fromCols(Collection)
// Groovy
static RowMatrix from(int size, Closure<? extends Number>)
// :note: jse 4.0.1 — from(nRows, nCols, Closure) 忽略 nCols 始终创建方阵（调用单参 fromDouble(aSize,closure)）
static RowMatrix from(int nRows, int nCols, Closure<? extends Number>)

// === 从 numpy NDArray 创建（自动检测类型，零拷贝） ===
static Object fromNumpy(NDArray<?> aNDArray, boolean unsignedWarning)
static Object fromNumpy(NDArray<?> aNDArray)

// === 对角矩阵 ===
static RowMatrix diag(IVector) / diag(int size, IVectorGetter)
static RowMatrix diag(double... diags) / diag(Collection<? extends Number>)
// Groovy: diag(int size, Closure<? extends Number>)

// === Boolean / Int 矩阵构造 ===
static RowLogicalMatrix fromBoolean(int size, ILogicalVectorGetter) / fromBoolean(ILogicalVector)
static RowIntMatrix fromInt(int size, IIntVectorGetter) / fromInt(IIntVector)
```
