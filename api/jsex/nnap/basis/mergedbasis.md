# MergedBasis

> `jsex.nnap.basis.MergedBasis`

**核心职能**：将多个 `MergeableBasis`（`SphericalChebyshev` 或 `Chebyshev`）合并为一个大基组。`rcut` 取最大值，`size` 为各子基组维度之和。允许同一元素使用多种描述符。

```java
MergedBasis(MergeableBasis... aMergedBasis)      // varargs 构造，至少 2 个
static MergedBasis load(int aTypeNum, Map aMap)  // 从 Map 反序列化
int mergeSize()                                  // 合并的子基组数量
void save(Map rSaveTo)                           // 序列化（type: "merge", basis: [...])
```
