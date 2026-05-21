# Triplet

> `jse.code.collection.Triplet`

**核心职能**：`implements ITriplet<A,B,C>`。泛型三元组的可变实现，包含 `mA` / `mB` / `mC` 公共字段。

```java
// === 字段 ===
A mA
B mB
C mC

// === 构造器 ===
Triplet(A, B, C)

// === ITriplet 接口实现 ===
A a()
B b()
C c()

// === 对象方法 ===
boolean equals(Object)
int hashCode()
String toString()
```
