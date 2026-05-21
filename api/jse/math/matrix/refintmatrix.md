# RefIntMatrix

> `jse.math.matrix.RefIntMatrix`

**核心职能**：`abstract class extends AbstractIntMatrix`。只读整数矩阵骨架，`set()` 抛出 `UnsupportedOperationException`。`newZeros_` 返回 `RowIntMatrix`。子类只需实现 `get`/`nrows`/`ncols`。

```java
protected final IIntMatrix newZeros_(int aRowNum, int aColNum)

// === 子类需实现的抽象方法 ===
abstract int get(int aRow, int aCol)
abstract int nrows()
abstract int ncols()

// === 只读约束 ===
void set(int aRow, int aCol, int aValue)                // throws UnsupportedOperationException
int getAndSet(int aRow, int aCol, int aValue)           // calls get() then set()
```
