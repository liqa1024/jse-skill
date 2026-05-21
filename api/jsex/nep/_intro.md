# `jsex.nep`
> NEP (Neuroevolution Potential) 神经演化势——基于 GPUMD NEP_CPU C++ 实现，通过 JIT 运行时编译为 native 库调用。支持 `nep3`/`nep4`/`nep5` 势文件及 ZBL/dipole/polarizability 变体。CPU 模式支持 double/single 精度，CUDA 模式固定 single。提供 `IPairPotential` 完整实现及 LAMMPS `pair_style jse` 集成（CPU/GPU）。

## 架构总览 (Architecture)

```
IPairPotential
  → NEP                          — NEP 势函数主类 (JIT 编译, CPU/CUDA)

LmpPlugin.Pair
  → PairNEP                      — LAMMPS NEP pair style (CPU)
    → PairNEP_gpu                — LAMMPS NEP pair style (GPU)
```
