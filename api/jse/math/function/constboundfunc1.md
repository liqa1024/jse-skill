# ConstBoundFunc1

> `jse.math.function.ConstBoundFunc1`

**核心职能**：一维常数边界数值函数，`final class extends VectorFunc1`。查询点超出定义域时 clamp 到最近的边界值（常数外推），避免外插野值。

```java
// === 静态工厂 ===
static ConstBoundFunc1 zeros(double aX0, double aDx, int aNx)

// === 构造方法 ===
ConstBoundFunc1(double aX0, double aDx, Vector aF)                      // 均匀网格
ConstBoundFunc1(IVector aX, IVector aF)                                  // 非均匀网格（插值型）

// === 求值 ===
double subs(double aX)                                                   // clamp 到 [x0, x0+(Nx-1)*dx]
int getINear(double aX)                                                  // 索引 clamp 到 [0, Nx-1]

// === 工厂（子类实现） ===
protected ConstBoundFunc1 newInstance_(double aX0, double aDx, Vector aData)
```
