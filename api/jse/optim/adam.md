# Adam

> `jse.optim.Adam`

**核心职能**：适合有一定随机性的目标函数。维护动量 `m_k` 和方差 `v_k` 的指数移动平均，带偏差校正 `(1-β^k)`，参数更新 `x ← x - η·m̂/(√v̂ + ε)`。构造器可选 η（默认 0.001）、β₁（默认 0.9）、β₂（默认 0.999）、ε（默认 1e-8）。

```java
Adam()
Adam(double aEta)
Adam(double aEta, double aBeta1, double aBeta2, double aEps)

Adam setLearningRate(double aLearningRate)
// IOptimizer + AbstractOptimizer 全部方法
```
