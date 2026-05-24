# ISettableAtomDataOperation

> `jse.atom.ISettableAtomDataOperation`

**核心职能**：`extends IAtomDataOperation`。增加 `2this` 系列的就地修改操作（不创建新数据，直接修改原数据）。

```java
// === 抽象方法（覆写 refSlice 返回 ISettableAtomData，新增 2this 系列） ===
// :note: Groovy 中列表直接匹配 List 重载，无需 `as int[]` 强转
ISettableAtomData refSlice(ISlice)                                // 返回可设置
ISettableAtomData refSlice(List<Integer>)                         // 返回可设置
ISettableAtomData refSlice(int[])                                 // 返回可设置
ISettableAtomData refSlice(IIndexFilter)                          // 返回可设置
void map2this(int nAtom, IUnaryFullOperator)                         // 就地映射
void mapType2this(int nAtom, IUnaryFullOperator<Integer,? super IAtom>) // 就地种类映射
void mapTypeRandom2this(IRandom, IVector)                             // 就地随机种类
void perturbXYZGaussian2this(IRandom, double)                         // 就地高斯扰动
void wrapPBC2this()                                                   // 就地 PBC 绕回
List<IntVector> clusterAnalyze(double rCut, boolean unwrap)           // 团簇分析+可选展开
void unwrapByCluster2this(double rCut)                                // 就地按团簇展开

// === 便捷方法（default） ===
void map2this/mapType2this(IUnaryFullOperator)                // → xxx2this(1, opt)
void mapTypeRandom2this(IVector/double.../IRandom,double...)  // 多重重载
void perturbXYZGaussian2this(double)                          // → xxx2this(RANDOM, sigma)
// :note: Groovy 脚本优先使用 perturbXYZ2this / wrap2this 简写
@VisibleForTesting void perturbXYZ2this(IRandom,double)/perturbXYZ2this(double)
@VisibleForTesting void wrap2this()                           // → wrapPBC2this()
```
