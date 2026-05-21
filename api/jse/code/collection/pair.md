# Pair

> `jse.code.collection.Pair`

**核心职能**：`implements IPair<A,B>`。泛型二元组的可变实现，包含 `mFirst` / `mSecond` 公共字段。

```java
// === 字段 ===
A mFirst
B mSecond

// === 构造器 ===
Pair(A, B)

// === IPair 接口实现 ===
A first()
B second()

// === 对象方法 ===
boolean equals(Object)
int hashCode()
String toString()
```
