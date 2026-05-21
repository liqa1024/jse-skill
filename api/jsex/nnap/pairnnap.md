# PairNNAP

> `jsex.nnap.PairNNAP`

**核心职能**：`extends LmpPlugin.Pair`。对应 LAMMPS `pair_style jse jsex.nnap.PairNNAP`。在 `coeff` 中解析 `pair_coeff * * path/to/model.json elem1 ... elemN`，初始化 NNAP 实例（CPU）并构建 LAMMPS type → NNAP type 映射。支持多元素每元素独立截断半径。`compute` 委托 `mNNAP.computeLammps` 执行 JIT native 计算。

```java
static class InitHelper {
    static boolean initialized()                // 是否已执行静态初始化（加载 SimpleJIT）
    static void init()                          // 手动触发静态初始化
}

// === LmpPlugin.Pair 重写 ===
void settings(String... aArgs)                  // centroidstress + 限制单次 coeff + 禁用 VirialFdotr
void initStyle()                                // 要求 newton pair on + full neighbor list
void compute()                                  // 委托 mNNAP.computeLammps(this)
void coeff(String... aArgs)                     // pair_coeff * * path/to/model.json elem1 ... elemN
double initOne(int i, int j)                    // 返回第 i 种元素的截断半径
void close()                                    // 释放 mNNAP、mTypeMap、mCutsq 等
```
