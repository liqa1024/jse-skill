# IOptimizer

> `jse.optim.IOptimizer`

> 此类标记为 `@ApiStatus.Experimental`

**核心职能**：定义优化器生命周期——设置参数引用（`setParameter`）、目标函数与梯度（`setLossFunc`/`setLossFuncGrad`）、线搜索开关（`setLineSearch`/`setNoLineSearch`）、回调钩子（日志/中断/参数更新）、学习率与执行控制。所有设置方法返回 `IOptimizer` 自身支持链式调用。含 4 个 `@FunctionalInterface` 内部接口。

```java
// === 函数式接口 ===
@FunctionalInterface interface ILossFunc { double call() }
@FunctionalInterface interface ILossFuncGrad { double call(Vector rGrad) }
@FunctionalInterface interface ILogPrinter { void call(int aStep, int aLineSearchStep, double aLoss, boolean aPrintLog) }
@FunctionalInterface interface IBreakChecker { boolean call(int aStep, double aLoss, double aLastLoss, Vector aParameterStep) }

// === 配置 (均返回 IOptimizer 自身) ===
IOptimizer setParameter(IVector aParameter)
IOptimizer setLossFunc(ILossFunc aLossFunc)
IOptimizer setLossFuncGrad(ILossFuncGrad aLossFuncGrad)
IOptimizer setLineSearch()                    // strong Wolfe 线搜索 (默认 c1=0.0001, c2=0.1, maxIter=10)
IOptimizer setNoLineSearch()
IOptimizer setLogPrinter(ILogPrinter aLogPrinter)
IOptimizer setBreakChecker(IBreakChecker aBreakChecker)
IOptimizer setParameterUpdater(Runnable aUpdater)
IOptimizer setLearningRate(double aLearningRate)

// === 执行 ===
void run(int aMaxStep, boolean aPrintLog)
void run(int aMaxStep)                        // 默认 aPrintLog=true

// === 状态管理 ===
void reset()                                  // 重置优化器内部状态 (默认空实现)
void markLossFuncChanged()                    // 标记损失函数变化，清空 loss/梯度缓存
void markParameterChanged()                   // 标记参数变化，清空所有缓存
```
