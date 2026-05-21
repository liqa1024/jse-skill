# LongArrayVector

> `jse.math.vector.LongArrayVector`

**核心职能**：`abstract class extends AbstractLongVector implements IDataShell<long[]>`。long 类型向量的数组层抽象，封装 `long[]` 内部存储，提供 IDataShell 接口设置/获取内部数据。子类需实现 `newZeros_()` 和 `getIfHasSameOrderData()`。

```java
// === 构造 ===
protected LongArrayVector(long[] aData)

// === IDataShell ===
void setInternalData(long[] aData)
long[] internalData()
int internalDataSize()

// === 运算器 ===
ILongVectorOperation operation()

// === 批量填充与导出 ===
void fill(long[] aData)
long[] data()

// === 拷贝 ===
LongArrayVector copy()

// === 子类需实现 ===
protected abstract LongArrayVector newZeros_(int aSize)
abstract long @Nullable[] getIfHasSameOrderData(Object aObj)

// 内部运算器实现
protected class LongArrayVectorOperation_ extends LongArrayVectorOperation {
    protected LongArrayVector thisVector_()
    protected LongArrayVector newVector_(int aSize)
}
```
