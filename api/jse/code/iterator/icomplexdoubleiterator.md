# IComplexDoubleIterator

> `jse.code.iterator.IComplexDoubleIterator`

**核心职能**：`extends IComplexDouble`。无装箱复数迭代器，通过 `real()`/`imag()` 获取当前分量，无需分配 `ComplexDouble` 对象。

```java
boolean hasNext()
void nextOnly()
double real()
double imag()
```
