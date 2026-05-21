# PairNEP_gpu

> `jsex.nep.PairNEP_gpu`

**核心职能**：`extends PairNEP`。对应 LAMMPS `pair_style jse jsex.nep.PairNEP_gpu`。覆盖 `initNEP` 使用 CUDA 架构初始化，`compute` 委托 `mNEP.computeLammpsCuda` 经由 `Lammps2Cuda → CUDA Compute → Cuda2Lammps` 三阶段 pipeline 执行 GPU 计算。继承 PairNEP 的 `coeff`/`settings`/`initStyle`/`close` 全部方法。

```java
static class InitHelper {
    static boolean initialized()                // 是否已执行静态初始化（加载 CudaJIT）
    static void init()                          // 手动触发静态初始化
}

void compute()                                  // 委托 mNEP.computeLammpsCuda(this)
```
