# AbstractSettableAtomDataOperation

> `jse.atom.AbstractSettableAtomDataOperation`

**核心职能**：`abstract class extends AbstractAtomDataOperation implements ISettableAtomDataOperation`。可设置原子数据运算器的抽象基类，实现 `ISettableAtomDataOperation` 全部 `2this` 就地修改方法。覆写 `refSlice` 返回 `ISettableAtomData`。

```java
// === 抽象方法（覆写协变返回） ===
protected abstract ISettableAtomData thisAtomData_()

// 从 AbstractAtomDataOperation 继承的抽象方法：
// newSameSettableAtomData_() / newSettableAtomData_(int) / newSettableAtomData_(int, IBox)

// === 覆写 refSlice 返回 ISettableAtomData ===
// :note: Groovy 脚本优先使用 List 重载，避免 `as int[]` 转换
ISettableAtomData refSlice(ISlice)
ISettableAtomData refSlice(List<Integer>)
ISettableAtomData refSlice(int[])
ISettableAtomData refSlice(IIndexFilter)

// === 2this 就地修改 ===
void map2this(int minTypeNum, IUnaryFullOperator<? extends IAtom, ? super IAtom>)
void mapType2this(int minTypeNum, IUnaryFullOperator<Integer, ? super IAtom>)
void mapTypeRandom2this(IRandom, IVector typeWeights)
void perturbXYZGaussian2this(IRandom, double sigma)
void wrapPBC2this()

// === 团簇分析 ===
List<IntVector> clusterAnalyze(double rCut, boolean unwrapByCluster)
void unwrapByCluster2this(double rCut)
```
