# PairNEP

> `jsex.nep.PairNEP`

**核心职能**：`extends LmpPlugin.Pair`。对应 LAMMPS `pair_style jse jsex.nep.PairNEP`。在 `coeff` 中解析 `pair_coeff * * path/to/nep.txt elem1 ... elemN`，初始化 NEP 实例（CPU 架构）并构建 LAMMPS type → NEP element 映射。`compute` 委托 `mNEP.computeLammps` 执行 JIT native 计算。

```java
static class InitHelper {
    static boolean initialized()                // 是否已执行静态初始化（加载 SimpleJIT）
    static void init()                          // 手动触发静态初始化
}

// === LmpPlugin.Pair 重写 ===
void settings(String... aArgs)                  // centroidstress + 限制单次 coeff + 禁用 VirialFdotr
void initStyle()                                // 要求 newton pair on + full neighbor list
void compute()                                  // 委托 mNEP.computeLammps(this)
void coeff(String... aArgs)                     // pair_coeff * * path/to/nep.txt elem1 ... elemN
double initOne(int i, int j)                    // 返回截断半径（用于 LAMMPS 近邻列表构建）
void close()                                    // 释放 mNEP、mTypeMap、mCutoffsq
```
