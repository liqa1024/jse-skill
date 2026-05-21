# MirrorBasis

> `jsex.nnap.basis.MirrorBasis`

**核心职能**：将一种元素的描述符计算完全委托给另一种元素（适用于化学性质相同的元素）。不产生额外可训练参数。

```java
MirrorBasis(Basis aMirrorBasis, int aMirrorType)  // aMirrorType 1-indexed
static MirrorBasis load(Basis[] aBasis, Map aMap)  // 从 Map 反序列化 ("mirror": N)
Basis mirrorBasis()                                // 返回被镜像的 Basis
int mirrorType()                                   // 返回镜像目标类型索引
void save(Map rSaveTo)                             // 序列化（type: "mirror"）
```
