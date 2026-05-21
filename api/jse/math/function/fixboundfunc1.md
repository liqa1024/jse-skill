# FixBoundFunc1

> `jse.math.function.FixBoundFunc1`

**核心职能**：一维固定边界数值函数，`final class extends VectorFunc1`。超出定义域时返回用户指定的固定边界值（左右可独立设置），通过链式 setter 配置。

```java
// === 静态工厂 ===
static FixBoundFunc1 zeros(double aX0, double aDx, int aNx)

// === 构造方法 ===
FixBoundFunc1(double aX0, double aDx, Vector aF)                         // 均匀网格，默认边界值 0.0
FixBoundFunc1(IVector aX, IVector aF)                                     // 插值型，默认边界值 0.0

// === 边界配置（链式） ===
FixBoundFunc1 setBound(double aBound)                                    // 左右同时设为相同值
FixBoundFunc1 setBound(double aBoundL, double aBoundR)                   // 左右独立设置

// === 求值 ===
double subs(double aX)                                                   // 超出区间返回 mBoundL / mBoundR
int getINear(double aX)                                                  // 索引 clamp 到 [0, Nx-1]

// === 工厂（子类实现，携带边界值） ===
protected FixBoundFunc1 newInstance_(double aX0, double aDx, Vector aData)
```
