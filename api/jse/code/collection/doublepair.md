# DoublePair

> `jse.code.collection.DoublePair`

**核心职能**：`implements IDoublePair`。double 专用二元组的可变实现，包含 `mFirst` / `mSecond` 公共字段。

```java
// === 字段 ===
double mFirst
double mSecond

// === 构造器 ===
DoublePair(double, double)

// === IDoublePair 接口实现 ===
double first()
double second()

// === 对象方法 ===
boolean equals(Object)
int hashCode()
String toString()
```
