# `jsex.nnap.basis`
> NNAP 基组（描述符）抽象层——将原子近邻环境映射为固定长度的描述符向量。提供 JIT 版本（`Chebyshev`/`SphericalChebyshev`/`MergedBasis`）和纯 Java 版本（`SimpleChebyshev`/`SimpleSphericalChebyshev`）。支持种类编码（wtype）、融合权重（fuse/post_fuse）、镜像（`MirrorBasis`）和共享（`SharedBasis`）等组合模式。

## 架构总览 (Architecture)

```
ISavable
  → Basis (@Experimental @Internal)             — JIT 基组抽象根类
    → MergedBasis                                — 多基组合并
    → MirrorBasis                                — 镜像包装 (引用另一元素的基组)
    → SharedBasis                                — 共享包装 (共享另一元素的基组参数)
    → MergeableBasis                             — 可合并基组抽象
      → WTypeBasis (package-private)             — 化学编码基组
        → Chebyshev                              — 径向基组 (Chebyshev 多项式)
        → SphericalChebyshev                     — 径向+角向基组 (默认)

SimpleBasis (@Experimental)                      — 纯 Java 基组抽象根类
  → SimpleChebyshev                              — 纯 Java 径向基组
  → SimpleSphericalChebyshev                     — 纯 Java 径向+角向基组
```
