# `jsex.nnap`
> NNAP (Neural Network Atomic Potential) 神经网络原子势——JIT 运行时编译 C++ 实现，支持多元素体系的描述符计算、能量/力/维里预测与训练。CPU 模式支持 double/single 精度，含实验性 CUDA 支持（已废弃）。提供 `IPairPotential` 完整实现、LAMMPS `pair_style jse` 集成及完整训练框架。

## 架构总览 (Architecture)

```
IPairPotential
  → NNAP (@Experimental)                      — NNAP 神经原子势主类 (JIT 编译, CPU)

LmpPlugin.Pair
  → PairNNAP                                  — LAMMPS NNAP pair style (CPU)
    → PairNNAP_gpu (@Obsolete)                — LAMMPS NNAP pair style (GPU, 已废弃)

IHasSymbol, ISavable, AutoCloseable
  → Trainer                                   — NNAP 训练器

NNAPExtensions (static)                       — APC 扩展: calBasisNNAP
```

> NNAP_cuda（`@ApiStatus.Experimental @ApiStatus.Obsolete`）、NNAPGEN 均为 package-private 内部实现。
