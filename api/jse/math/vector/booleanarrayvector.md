# BooleanArrayVector

> `jse.math.vector.BooleanArrayVector`

**核心职能**：`abstract class extends AbstractLogicalVector implements IDataShell<boolean[]>`。boolean 类型（逻辑）向量的数组层抽象，封装 `boolean[]` 内部存储，提供 IDataShell 接口设置/获取内部数据。子类需实现 `newZeros_()` 和 `getIfHasSameOrderData()`。

```java
// === 构造 ===
protected BooleanArrayVector(boolean[] aData)

// === IDataShell ===
void setInternalData(boolean[] aData)
boolean[] internalData()
int internalDataSize()

// === 运算器 ===
ILogicalVectorOperation operation()

// === 批量填充与导出 ===
void fill(boolean[] aData)
boolean[] data()

// === 子类需实现 ===
protected abstract BooleanArrayVector newZeros_(int aSize)
abstract boolean @Nullable[] getIfHasSameOrderData(Object aObj)

// 内部运算器实现
protected class BooleanArrayVectorOperation_ extends BooleanArrayVectorOperation {
    protected BooleanArrayVector thisVector_()
    protected BooleanArrayVector newVector_(int aSize)
}
```
