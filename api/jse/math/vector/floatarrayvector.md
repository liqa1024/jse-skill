# FloatArrayVector

> `jse.math.vector.FloatArrayVector`

**核心职能**：`abstract class extends AbstractFloatVector implements IDataShell<float[]>`。内部存储 `float[]` 的向量基类，为子类提供 `IDataShell` 接口及批量 `fill`/`data`/`copy` 优化。

```java
// === IDataShell ===
void setInternalData(float[] aData)
float[] internalData()
int internalDataSize()
abstract float @Nullable[] getIfHasSameOrderData(Object aObj)

// === 运算入口 ===
IFloatVectorOperation operation()

// === 批量优化 ===
void fill(float[] aData)
float[] data()
FloatArrayVector copy()

// === 子类需实现 ===
protected abstract FloatArrayVector newZeros_(int aSize)

// === 内部运算类 ===
protected class FloatArrayVectorOperation_ extends FloatArrayVectorOperation {
    protected FloatArrayVector thisVector_()
    protected FloatArrayVector newVector_(int aSize)
}
```
