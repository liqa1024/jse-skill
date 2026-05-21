# `jse.atom`

> 分子模拟核心包——定义原子/坐标/模拟盒/键的数据结构，提供原子数据容器、结构分析、势函数计算。按 8 条继承链组织。

## 架构总览 (Architecture)

```
IXYZ → ISettableXYZ → IAtom → ISettableAtom       ← 坐标→原子继承链
IBox                                                  ← 模拟盒（extends IXYZ）
IHasSymbol → IAtomData → ISettableAtomData            ← 原子数据容器链
IAtomDataOperation → ISettableAtomDataOperation       ← 数据运算器链（Operation 模式）
IPotential → IPairPotential                           ← 势函数链（extends AutoCloseable）
IBond                                                  ← 键（独立，@ApiStatus.Experimental）
```
