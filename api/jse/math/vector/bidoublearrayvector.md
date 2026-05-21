# BiDoubleArrayVector

> `jse.math.vector.BiDoubleArrayVector`

**核心职能**：`abstract class extends AbstractComplexVector implements IDataShell<double[][]>`。复类型向量的数组层抽象，使用 `double[2][]` 交错存储（第 0 行实部、第 1 行虚部）。提供 IDataShell 接口设置/获取内部数据。子类需实现 `newZeros_()` 和 `getIfHasSameOrderData()`。

```java
// === 构造 ===
protected BiDoubleArrayVector(double[][] aData)

// === IDataShell ===
void setInternalData(double[][] aData)
double[][] internalData()
int internalDataSize()

// === 运算器 ===
IComplexVectorOperation operation()

// === 批量填充与导出 ===
void fill(double[][] aData)
void fill(double[] aData)
double[][] data()

// === 子类需实现 ===
protected abstract BiDoubleArrayVector newZeros_(int aSize)
abstract double @Nullable[][] getIfHasSameOrderData(Object aObj)

// 内部运算器实现
protected class BiDoubleArrayVectorOperation_ extends BiDoubleArrayVectorOperation {
    protected BiDoubleArrayVector thisVector_()
    protected BiDoubleArrayVector newVector_(int aSize)
}
```
