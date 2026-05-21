# BooleanArrayMatrix

> `jse.math.matrix.BooleanArrayMatrix`

**核心职能**：`abstract class extends AbstractLogicalMatrix implements IDataShell<boolean[]>`。内部以 `boolean[]` 存储的矩阵，提供底层数组的直接读写能力，为 `ARRAY` 优化路径提供数据支撑。内部类 `BooleanArrayMatrixOperation_` 连接运算层。

```java
// === DataShell 接口 ===
void setInternalData(boolean[] aData)
boolean[] internalData()
int internalDataSize()

// === 内部运算器 ===
protected class BooleanArrayMatrixOperation_ extends BooleanArrayMatrixOperation {
    protected BooleanArrayMatrix thisMatrix_()
    protected BooleanArrayMatrix newMatrix_(int aRowNum, int aColNum)
}

// === 覆写 / 拷贝 ===
protected final ILogicalVector newZerosVec_(int aSize)
BooleanArrayMatrix copy()

// === 子类需覆写 ===
protected abstract BooleanArrayMatrix newZeros_(int aRowNum, int aColNum)
abstract boolean @Nullable[] getIfHasSameOrderData(Object aObj)
```
