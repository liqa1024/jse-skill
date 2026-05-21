# LBFGS

> `jse.optim.LBFGS`

**核心职能**：限制内存拟牛顿法，维护最近 m 步的 `s_k`/`y_k`/`ρ_k` 历史（默认 m=20），通过双循环递归逼近 Hessian 逆矩阵 × 梯度的方向。数值稳定性保护（`dot(s,y) > 1e-10` 才更新历史）。线搜索默认使用 c₂=0.9（较宽松的 Wolfe 条件）。无线搜索时学习率随已用记忆量递增（`η + used²·ηinc`，上限 1.0）。

```java
LBFGS()
LBFGS(int aM)                                 // aM: 记忆长度, 默认 20

LBFGS setLearningRate(double aLearningRate)
LBFGS setLineSearch()                         // wolfe c2 改为 0.9
// IOptimizer + AbstractOptimizer 全部方法
```
