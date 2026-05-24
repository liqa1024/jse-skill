# AbstractAtomDataOperation

> `jse.atom.AbstractAtomDataOperation`

**核心职能**：`abstract class implements IAtomDataOperation`。原子数据运算器的抽象基类，实现 `IAtomDataOperation` 全部方法（过滤/映射/切片/扰动/扩胞/团簇）。子类需提供数据创建能力的四个抽象方法。

```java
// === 抽象方法（子类必须实现） ===
protected abstract IAtomData thisAtomData_()
protected abstract ISettableAtomData newSameSettableAtomData_()
protected abstract ISettableAtomData newSettableAtomData_(int atomNum)
protected abstract ISettableAtomData newSettableAtomData_(int atomNum, IBox)

// === 过滤 ===
ISettableAtomData filter(IFilter<IAtom>)
ISettableAtomData filterType(int aType)

// === 引用切片（返回 IAtomData 视图） ===
// :note: 半弃用 — 命名与 slice() 易混淆，使用频率低
// :note: Groovy 中列表直接匹配 List 重载，无需 `as int[]` 强转
IAtomData refSlice(ISlice)
IAtomData refSlice(List<Integer>)
IAtomData refSlice(int[])
IAtomData refSlice(IIndexFilter)

// === 映射 ===
ISettableAtomData map(int minTypeNum, IUnaryFullOperator<? extends IAtom, ? super IAtom>)
ISettableAtomData mapType(int minTypeNum, IUnaryFullOperator<Integer, ? super IAtom>)
ISettableAtomData mapTypeRandom(IRandom, IVector typeWeights)

// === 扰动与周期边界 ===
ISettableAtomData perturbXYZGaussian(IRandom, double sigma)
ISettableAtomData wrapPBC()

// === 扩胞与分块 ===
ISettableAtomData repeat(int nx, int ny, int nz)
List<? extends ISettableAtomData> slice(int nx, int ny, int nz)

// === 团簇分析 ===
List<IntVector> clusterAnalyze(double rCut)
ISettableAtomData unwrapByCluster(double rCut)
protected List<IntVector> clusterAnalyze_(double rCut, boolean unwrap, boolean outputIndex)
```
