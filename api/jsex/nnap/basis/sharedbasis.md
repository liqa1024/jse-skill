# SharedBasis

> `jsex.nnap.basis.SharedBasis`

**核心职能**：共享另一元素的基组参数（但种类编码保持独立）。不产生额外可训练参数。

```java
SharedBasis(Basis aSharedBasis, int aSharedType)   // aSharedType 1-indexed
static SharedBasis load(Basis[] aBasis, Map aMap)  // 从 Map 反序列化 ("share": N)
Basis sharedBasis()                                // 返回被共享的 Basis
int sharedType()                                   // 返回共享目标类型索引
void save(Map rSaveTo)                             // 序列化（type: "share"）
```
