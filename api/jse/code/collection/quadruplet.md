# Quadruplet

> `jse.code.collection.Quadruplet`

**核心职能**：`implements IQuadruplet<A,B,C,D>`。泛型四元组的可变实现，包含 `mA` / `mB` / `mC` / `mD` 公共字段。

```java
// === 字段 ===
A mA
B mB
C mC
D mD

// === 构造器 ===
Quadruplet(A, B, C, D)

// === IQuadruplet 接口实现 ===
A a()
B b()
C c()
D d()

// === 对象方法 ===
boolean equals(Object)
int hashCode()
String toString()
```
