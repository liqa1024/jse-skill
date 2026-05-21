# IntArrayVector

> `jse.math.vector.IntArrayVector`

**核心职能**：`abstract class extends AbstractIntVector implements IDataShell<int[]>`。内部存储 `int[]` 的向量基类，为子类提供 `IDataShell` 接口及批量 `fill`/`data`/`copy` 优化。

```java
// === IDataShell ===
void setInternalData(int[] aData)
int[] internalData()
int internalDataSize()
abstract int @Nullable[] getIfHasSameOrderData(Object aObj)

// === 运算入口 ===
IIntVectorOperation operation()

// === 批量优化 ===
void fill(int[] aData)
int[] data()
IntArrayVector copy()

// === 子类需实现 ===
protected abstract IntArrayVector newZeros_(int aSize)

// === 内部运算类 ===
protected class IntArrayVectorOperation_ extends IntArrayVectorOperation {
    protected IntArrayVector thisVector_()
    protected IntArrayVector newVector_(int aSize)
}
```
