# IComplexMatrixGetter

> `jse.math.matrix.IComplexMatrixGetter`

**核心职能**：`@FunctionalInterface`。复数矩阵元素访问抽象，通过 `get()` 返回复数对象，`getReal()`/`getImag()` 直接取实虚部。

```java
@FunctionalInterface

IComplexDouble get(int aRow, int aCol)
default double getReal(int aRow, int aCol)
default double getImag(int aRow, int aCol)
```
