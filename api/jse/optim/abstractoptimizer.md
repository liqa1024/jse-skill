# AbstractOptimizer

> `jse.optim.AbstractOptimizer`

**核心职能**：模板方法模式实现优化主循环。内置 loss/梯度延迟计算与缓存（`eval`/`grad`/`loss`/`invalidLoss`），strong Wolfe 线搜索（二次样条插值选择步长），默认日志打印（含线搜索步数），默认收敛检测（`DBL_EPSILON` 相对变化）。子类需重写 `calStep` 定义参数更新方向，可选重写 `lineSearchAlways`/`updateLearningRate`/`applyStep`/`printLog`/`checkBreak`。

```java
// === 构造后配置 (返回 AbstractOptimizer 自身) ===
AbstractOptimizer setLineSearchStrongWolfe(double aC1, double aC2, int aMaxIter)

// === 缓存管理 (protected) ===
protected double eval(boolean aRequireGrad)    // 计算损失值，aRequireGrad=true 时同时计算梯度
protected double eval()                        // 计算损失值 (不要求梯度)
protected Vector grad()                        // 获取梯度 (缓存不合法时自动重算)
protected double loss()                        // 获取 loss (缓存不合法时自动重算)
protected void invalidLoss()                   // 清空 loss/梯度缓存

// === 模板方法钩子 (protected, 子类重写) ===
protected abstract void calStep(int aStep, IVector aParameter, Vector rParameterStep)
protected int lineSearch(int aStep, double aLoss, IVector rParameter, Vector rParameterStep)
protected double lineSearchChoose(double aAlphaL, double aAlphaR, double aLossL, double aLossR, double aGradL)
protected boolean lineSearchAlways()           // 是否始终执行一次线搜索 (默认 false)
protected void updateLearningRate(double aLR)  // 线搜索后更新学习率 (默认空)
protected void applyStep(int aStep)            // 应用步长 (默认 mParameter += mParameterStep)
protected void printLog(int aStep, int aLineSearchStep, double aLoss, boolean aPrintLog)
protected boolean checkBreak(int aStep, double aLoss, double aLastLoss, Vector aParameterStep)
protected void updateParameter()               // 触发参数更新钩子
protected void checkSetting()                  // 验证必要设置已完成
```
