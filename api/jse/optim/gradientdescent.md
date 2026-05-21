# GradientDescent

> `jse.optim.GradientDescent`

**核心职能**：`x ← x - η·∇f`。构造器可选学习率（默认 0.1），支持 `setLearningRate` 动态调整。

```java
GradientDescent()
GradientDescent(double aEta)

GradientDescent setLearningRate(double aLearningRate)
// IOptimizer 全部方法
```
