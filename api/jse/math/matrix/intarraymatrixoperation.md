# IntArrayMatrixOperation

> `jse.math.matrix.IntArrayMatrixOperation`

**核心职能**：`abstract class extends AbstractIntMatrixOperation`。int 数组运算层，`fill` 方法采用 ARRAY/DATA 双路径优化：如果 RHS 共享相同底层数组布局则走 `ARRAY.ebeFill2This` 零拷贝路径，否则回退 `DATA.ebeFill2This` 迭代器路径。

```java
// === 填充（双路径优化） ===
void fill(int aRHS)                             // ARRAY.mapFill2This
void fill(IIntMatrix aRHS)                      // ARRAY 零拷贝 或 DATA 回退

// === 子类需覆写 ===
protected abstract IntArrayMatrix thisMatrix_()
protected abstract IntArrayMatrix newMatrix_(int aRowNum, int aColNum)
```
