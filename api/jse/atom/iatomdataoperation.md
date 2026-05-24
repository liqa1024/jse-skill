# IAtomDataOperation

> `jse.atom.IAtomDataOperation`

**核心职能**：在不可变 `IAtomData` 上执行过滤/映射/切片/扰动/扩胞/团簇分析等操作，返回新的 `ISettableAtomData`。无基底接口。

```java
// === 抽象方法 ===
ISettableAtomData filter(IFilter<IAtom>)                       // 通用过滤器
ISettableAtomData filterType(int aType)                        // 按种类过滤保留
// :note: 半弃用 — 命名与 slice() 易混淆，使用频率低
// :note: Groovy 中列表直接匹配 List 重载，无需 `as int[]` 强转
IAtomData refSlice(ISlice)                                       // 引用切片（非拷贝）
IAtomData refSlice(List<Integer>)                                // 引用切片（非拷贝）
IAtomData refSlice(int[])                                        // 引用切片（非拷贝）
IAtomData refSlice(IIndexFilter)                                 // 引用切片（非拷贝）
ISettableAtomData map(int nAtom, IUnaryFullOperator)           // 每 nAtom 组映射
ISettableAtomData mapType(int nAtom, IUnaryFullOperator<Integer,? super IAtom>) // 种类映射
ISettableAtomData mapTypeRandom(IRandom, IVector aWeights)     // 按权重随机分配种类
ISettableAtomData perturbXYZGaussian(IRandom, double aSigma)   // 高斯扰动坐标
ISettableAtomData wrapPBC()                                    // 周期边界条件绕回
ISettableAtomData repeat(int nx, int ny, int nz)               // 超胞扩胞
List<? extends ISettableAtomData> slice(int nx, int ny, int nz)// 分块
List<IntVector> clusterAnalyze(double rCut)                    // 团簇分析（返回索引列表）
ISettableAtomData unwrapByCluster(double rCut)                 // 按团簇展开 PBC

// === 便捷方法（default，委托到抽象方法） ===
ISettableAtomData map(IUnaryFullOperator)                      // → map(1, opt)
ISettableAtomData mapType(IUnaryFullOperator)                  // → mapType(1, opt)
ISettableAtomData mapTypeRandom(double... weights)             // → mapTypeRandom(RANDOM, ...)
ISettableAtomData mapTypeRandom(IRandom, double... weights)    // → mapTypeRandom(rng, Vectors.from(weights))
ISettableAtomData mapTypeRandom(IVector weights)               // → mapTypeRandom(RANDOM, weights)
ISettableAtomData perturbXYZGaussian(double sigma)             // → perturbXYZGaussian(RANDOM, sigma)
ISettableAtomData repeat(int aN)                               // → repeat(aN, aN, aN)
List<? extends ISettableAtomData> slice(int aN)                // → slice(aN, aN, aN)
// :note: Groovy 脚本优先使用 perturbXYZ / wrap 简写
@VisibleForTesting ISettableAtomData perturbXYZ(IRandom,double)// → perturbXYZGaussian
@VisibleForTesting ISettableAtomData perturbXYZ(double)        // → perturbXYZGaussian
@VisibleForTesting ISettableAtomData wrap()                    // → wrapPBC()
```
