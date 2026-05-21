# AbstractAtom

> `jse.atom.AbstractAtom`

**核心职能**：`abstract class implements IAtom`。统一 `toString()` 格式（根据 hasID/hasVelocity 条件输出不同字段）并提供 `copy()` 默认实现。

```java
String toString()               // 条件格式化的原子信息字符串
ISettableAtom copy()            // 根据 hasVelocity/hasID 返回 AtomFull/AtomID/Atom
```
