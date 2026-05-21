# RefComplexVector

> `jse.math.vector.RefComplexVector`

**核心职能**：`abstract class extends AbstractComplexVector`。复类型向量的引用视图基类。子类只需实现 `getReal()`、`getImag()` 和 `size()`；`setReal()` 和 `setImag()` 默认抛出 `UnsupportedOperationException("set")`，适用于不可变/只读向量视图。`newZeros_()` 委托给 `ComplexVector.zeros()`。

```java
// === 子类需实现 ===
abstract double getReal(int aIdx)
abstract double getImag(int aIdx)
abstract int size()

// === 默认行为 ===
void set(int aIdx, double aReal, double aImag)  // setReal + setImag 组合
void setReal(int aIdx, double aReal)                // throws UnsupportedOperationException
void setImag(int aIdx, double aImag)                // throws UnsupportedOperationException
ComplexDouble getAndSet(int aIdx, double aReal, double aImag) // getAndSetReal + getAndSetImag 组合
double getAndSetReal(int aIdx, double aReal)       // getReal + setReal 组合
double getAndSetImag(int aIdx, double aImag)       // getImag + setImag 组合
```
