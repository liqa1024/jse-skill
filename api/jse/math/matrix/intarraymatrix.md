# IntArrayMatrix

> `jse.math.matrix.IntArrayMatrix`

**核心职能**：`abstract class extends AbstractIntMatrix implements IDataShell<int[]>`。内部以 `int[]` 存储的矩阵，提供底层数组的直接读写能力，为 `ARRAY` 优化路径提供数据支撑。内部类 `IntArrayMatrixOperation_` 连接运算层。

```java
// === DataShell 接口 ===
void setInternalData(int[] aData)
int[] internalData()
int internalDataSize()

// === 内部运算器 ===
protected class IntArrayMatrixOperation_ extends IntArrayMatrixOperation {
    protected IntArrayMatrix thisMatrix_()
    protected IntArrayMatrix newMatrix_(int aRowNum, int aColNum)
}

// === 覆写 / 拷贝 ===
protected final IIntVector newZerosVec_(int aSize)
IntArrayMatrix copy()

// === 子类需覆写 ===
protected abstract IntArrayMatrix newZeros_(int aRowNum, int aColNum)
abstract int @Nullable[] getIfHasSameOrderData(Object aObj)
```
