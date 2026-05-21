# BiDoubleArrayMatrix

> `jse.math.matrix.BiDoubleArrayMatrix`

**核心职能**：`abstract class extends AbstractComplexMatrix implements IDataShell<double[][]>`。内部以 `double[2][]`（第 0 维=实部/虚部）存储的复数矩阵，提供底层双精度数组的直接读写能力。内部类 `BiDoubleArrayMatrixOperation_` 将 `operation()` 返回具体运算器类型。

```java
// === DataShell 接口 ===
void setInternalData(double[][] aData)
double[][] internalData()
int internalDataSize()

// === 内部运算器 ===
protected class BiDoubleArrayMatrixOperation_ extends BiDoubleArrayMatrixOperation {
    protected BiDoubleArrayMatrix thisMatrix_()
    protected BiDoubleArrayMatrix newMatrix_(int aRowNum, int aColNum)
}
IComplexMatrixOperation operation()                     // 返回 BiDoubleArrayMatrixOperation_

// === 覆写 / 拷贝 ===
protected final IComplexVector newZerosVec_(int aSize)
BiDoubleArrayMatrix copy()

// === 子类需覆写 ===
protected abstract BiDoubleArrayMatrix newZeros_(int aRowNum, int aColNum)
abstract double @Nullable[][] getIfHasSameOrderData(Object aObj)
```
