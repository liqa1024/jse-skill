# ConstBoundFunc2

> `jse.math.function.ConstBoundFunc2`

**核心职能**：二维常数边界数值函数，`final class extends ColumnMatrixFunc2`。XY 两个方向各自独立 clamp 到最邻近边界值（常数外推）。

```java
// === 静态工厂 ===
static ConstBoundFunc2 zeros(double aX0, double aDx, int aN)            // 正方形均匀网格
static ConstBoundFunc2 zeros(double aX0, double aY0, double aDx, double aDy, int aNx, int aNy)

// === 构造方法 ===
ConstBoundFunc2(double aX0, double aY0, double aDx, double aDy, ColumnMatrix aData)

// === 求值 ===
double subs(double aX, double aY)                                        // 双线性插值，边界 clamp
int getINear(double aX)                                                  // x 索引 clamp 到 [0, Nx-1]
int getJNear(double aY)                                                  // y 索引 clamp 到 [0, Ny-1]

// === 工厂（子类实现） ===
protected ConstBoundFunc2 newInstance_(double aX0, double aY0, double aDx, double aDy, ColumnMatrix aData)
```
