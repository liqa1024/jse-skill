# RefMatrix

> `jse.math.matrix.RefMatrix`

**核心职能**：`abstract class extends AbstractMatrix`。只读实数矩阵骨架，`set()` 抛出 `UnsupportedOperationException`。`newZeros_` 返回 `RowMatrix`。子类只需实现 `get`/`nrows`/`ncols`。

```java
protected final IMatrix newZeros_(int aRowNum, int aColNum)

// === 子类需实现的抽象方法 ===
abstract double get(int aRow, int aCol)
abstract int nrows()
abstract int ncols()

// === 只读约束 ===
void set(int aRow, int aCol, double aValue)              // throws UnsupportedOperationException
double getAndSet(int aRow, int aCol, double aValue)      // calls get() then set()
```
