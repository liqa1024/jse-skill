# ZeroBoundFunc1

> `jse.math.function.ZeroBoundFunc1`

**核心职能**：一维零边界数值函数，`final class extends VectorFunc1 implements IZeroBoundFunc1`。查询点超出定义域时返回 `0.0`，适合配合零边界微分/积分/卷积裁剪优化。

```java
// === 静态工厂 ===
static ZeroBoundFunc1 zeros(double aX0, double aDx, int aNx)

// === 构造方法 ===
ZeroBoundFunc1(double aX0, double aDx, Vector aF)                        // 均匀网格
ZeroBoundFunc1(IVector aX, IVector aF)                                    // 插值型

// === 求值 ===
double subs(double aX)                                                   // 超出区间返回 0.0
int getINear(double aX)                                                  // 索引 clamp 到 [0, Nx-1]

// === 零边界标记（IZeroBoundFunc1） ===
double zeroBoundL()                                                      // 左侧零边界位置：x0 - dx
double zeroBoundR()                                                      // 右侧零边界位置：x0 + Nx * dx

// === 工厂（子类实现） ===
protected ZeroBoundFunc1 newInstance_(double aX0, double aDx, Vector aData)
```
