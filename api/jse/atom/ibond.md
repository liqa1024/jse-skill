# IBond

> `jse.atom.IBond`

**核心职能**：定义化学键的只读协议（种类号、连接原子索引、连接的原子引用）。无基底接口。标注 `@ApiStatus.Experimental`。

> `@ApiStatus.Experimental`

```java
// === 抽象方法 ===
int type()                      // 键的种类编号，从 1 开始
int bondIndex()                 // 连接的目标原子在 AtomData 中的索引
IAtom bondAtom()                // 连接的目标原子引用

// === 可选属性（default） ===
int id()                        // 键的 id，默认 -1
boolean hasID()                 // 是否包含真实 id，默认 false
```
