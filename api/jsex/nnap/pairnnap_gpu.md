# PairNNAP_gpu

> `jsex.nnap.PairNNAP_gpu`

> 此类标记为 `@ApiStatus.Obsolete`

**核心职能**：`extends PairNNAP`。对应 LAMMPS `pair_style jse jsex.nnap.PairNNAP_gpu`。覆盖 `initNNAP` 使用 `NNAP_cuda`（GPU 架构，当前标记为废弃）。继承 PairNNAP 的 `coeff`/`settings`/`initStyle`/`close` 全部方法。

```java
static class InitHelper {
    static boolean initialized()                // 是否已执行静态初始化（加载 CudaJIT）
    static void init()                          // 手动触发静态初始化
}
```
