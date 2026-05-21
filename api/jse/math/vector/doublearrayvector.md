# DoubleArrayVector

> `jse.math.vector.DoubleArrayVector`

**核心职能**：`abstract class extends AbstractVector implements IDataShell<double[]>`。内部存储 `double[]` 的向量基类，为子类提供 `IDataShell` 接口及批量 `fill`/`data`/`copy` 优化。

```java
// === IDataShell ===
void setInternalData(double[] aData)
double[] internalData()
int internalDataSize()
abstract double @Nullable[] getIfHasSameOrderData(Object aObj)

// === 运算入口 ===
IVectorOperation operation()

// === 批量优化 ===
void fill(double[] aData)
double[] data()
DoubleArrayVector copy()

// === 子类需实现 ===
protected abstract DoubleArrayVector newZeros_(int aSize)

// === 内部运算类 ===
protected class DoubleArrayVectorOperation_ extends DoubleArrayVectorOperation {
    protected DoubleArrayVector thisVector_()
    protected DoubleArrayVector newVector_(int aSize)
}
```
