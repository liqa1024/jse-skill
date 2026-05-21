# RefLogicalMatrix

> `jse.math.matrix.RefLogicalMatrix`

**核心职能**：`abstract class extends AbstractLogicalMatrix`。只读逻辑矩阵骨架，`set()` 抛出 `UnsupportedOperationException`。`newZeros_` 返回 `RowLogicalMatrix`。子类只需实现 `get`/`nrows`/`ncols`。

```java
protected final ILogicalMatrix newZeros_(int aRowNum, int aColNum)

// === 子类需实现的抽象方法 ===
abstract boolean get(int aRow, int aCol)
abstract int nrows()
abstract int ncols()

// === 只读约束 ===
void set(int aRow, int aCol, boolean aValue)            // throws UnsupportedOperationException
boolean getAndSet(int aRow, int aCol, boolean aValue)   // calls get() then set()
```
