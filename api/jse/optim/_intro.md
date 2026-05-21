# `jse.optim`

> `@ApiStatus.Experimental` 通用数值优化框架——不限于原子结构优化，可用于任意可微目标函数。核心理念：设置参数引用（`IVector`）、损失函数（`ILossFunc`/`ILossFuncGrad`），迭代优化直接修改参数。支持 strong Wolfe 线搜索、自定义日志/中断/参数更新回调。内置 4 种优化器：GradientDescent、Adam、ConjugateGradient（Polak-Ribiere）、LBFGS。

## 架构总览 (Architecture)

```
IOptimizer (@ApiStatus.Experimental)
  ├─ ILossFunc         — 目标函数 (double call())
  ├─ ILossFuncGrad     — 目标函数+梯度 (double call(Vector rGrad))
  ├─ ILogPrinter       — 日志回调 (call(step, lineSearchStep, loss, printLog))
  └─ IBreakChecker     — 中断检测 (call(step, loss, lastLoss, paramStep))

AbstractOptimizer (abstract, implements IOptimizer)
  → GradientDescent     — 最简梯度下降 x ← x - η·∇f
  → Adam                — 自适应动量优化器 (动量+方差+偏差校正)
  → ConjugateGradient   — Polak-Ribiere 共轭梯度 (自适应 η, 始终线搜索)
  → LBFGS               — 限制内存拟牛顿法 (双循环递归, 可配记忆长度)
```
