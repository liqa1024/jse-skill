# ConjugateGradient

> `jse.optim.ConjugateGradient`

**核心职能**：采用 Polak-Ribiere 变体（与 LAMMPS 一致），`β = r_{k+1}·(r_{k+1}-r_k) / (r_k·r_k)`，β<0 时自动重置为最速下降。构造时默认开启线搜索（CG 收敛速度依赖精确线搜索）。支持自适应学习率调整（`setAdaptiveEta`，线搜索 α>1.5 时 η×1.5，α<0.7 时 η×0.7）。始终执行一次初始线搜索（`lineSearchAlways()=true`）。

```java
ConjugateGradient()
ConjugateGradient(double aEta)

ConjugateGradient setLearningRate(double aLearningRate)
ConjugateGradient setAdaptiveEta(boolean aAdaptiveEta)
// IOptimizer + AbstractOptimizer 全部方法
```
