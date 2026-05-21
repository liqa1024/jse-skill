# RefComplexMatrix

> `jse.math.matrix.RefComplexMatrix`

**核心职能**：`abstract class extends AbstractComplexMatrix`。只读复数矩阵骨架，`setReal`/`setImag` 抛出 `UnsupportedOperationException`。`newZeros_` 返回 `RowComplexMatrix`。子类只需实现 `getReal`/`getImag`/`nrows`/`ncols`。

```java
protected final IComplexMatrix newZeros_(int aRowNum, int aColNum)

// === 子类需实现的抽象方法 ===
abstract double getReal(int aRow, int aCol)
abstract double getImag(int aRow, int aCol)
abstract int nrows()
abstract int ncols()

// === 只读约束 ===
void set(int aRow, int aCol, double aReal, double aImag)     // calls setReal then setImag
void setReal(int aRow, int aCol, double aReal)               // throws UnsupportedOperationException
void setImag(int aRow, int aCol, double aImag)               // throws UnsupportedOperationException
ComplexDouble getAndSet(int aRow, int aCol, double aReal, double aImag)  // calls getAndSetReal / getAndSetImag
double getAndSetReal(int aRow, int aCol, double aReal)       // calls getReal() then setReal()
double getAndSetImag(int aRow, int aCol, double aImag)       // calls getImag() then setImag()
```
