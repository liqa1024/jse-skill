# DoubleArrayMatrix

> `jse.math.matrix.DoubleArrayMatrix`

**核心职能**：`abstract class extends AbstractMatrix implements IDataShell<double[]>`。内部持有 `double[] mData` 的矩阵骨架，运算通过 `DoubleArrayMatrixOperation_` 内部类启用 ARRAY 加速路径。子类只需实现 `newZeros_` 和 `getIfHasSameOrderData`。

```java
// === 字段 ===
protected double[] mData

// === 构造 ===
protected DoubleArrayMatrix(double[] aData)

// === IDataShell 实现 ===
void setInternalData(double[] aData)
double[] internalData()
int internalDataSize()

// === 运算器（覆写为 DoubleArrayMatrixOperation_）===
IMatrixOperation operation()

// === 零向量（final 禁止子类修改）===
protected final IVector newZerosVec_(int aSize)

// === 拷贝 ===
DoubleArrayMatrix copy()

// === 子类需实现的抽象方法 ===
protected abstract DoubleArrayMatrix newZeros_(int aRowNum, int aColNum)
abstract @Nullable double[] getIfHasSameOrderData(Object aObj)

// === 内部类 ===
protected class DoubleArrayMatrixOperation_ extends DoubleArrayMatrixOperation {
    protected DoubleArrayMatrix thisMatrix_()
    protected DoubleArrayMatrix newMatrix_(int aRowNum, int aColNum)
}
```
