# IDoubleIterator

> `jse.code.iterator.IDoubleIterator`

**核心职能**：无装箱 double 迭代器，提供 `toIterator()`→JDK Iterator、`forEachRemaining`、`remove` 默认方法，以及 `asDouble()`/`asInt()` 跨类型转换。

```java
boolean hasNext()
double next()
```
