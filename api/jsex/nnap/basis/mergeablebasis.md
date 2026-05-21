# MergeableBasis

> `jsex.nnap.basis.MergeableBasis`

**核心职能**：可被 `MergedBasis` 合并的基组抽象，`implements ISavable`。与 `Basis` 类似但 `updateGenMap`/`hasSameGenMap` 签名含额外的 `aGenIdxType`/`aGenIdxMerge` 参数用于合并场景下的代码生成。

```java
// 与 Basis 相同的参数/梯度/缓存协议，额外含：
void mountCptrHyperParameter(IDoubleOrFloatCPointer aPtr) // 设置 rcut
int cptrHyperParameterSize()                               // 返回 1
abstract void updateGenMap(Map<String, Object> rGenMap, int aGenIdxType, int aGenIdxMerge)
abstract boolean hasSameGenMap(MergeableBasis aBasis)
```
