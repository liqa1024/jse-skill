# ZeroBoundFunc2

> `jse.math.function.ZeroBoundFunc2`

**核心职能**：二维零边界数值函数，`final class extends ColumnMatrixFunc2 implements IZeroBoundFunc2`。XY 任一方向超出定义域时返回 `0.0`。

```java
// === 静态工厂 ===
static ZeroBoundFunc2 zeros(double aX0, double aDx, int aN)             // 正方形均匀网格
static ZeroBoundFunc2 zeros(double aX0, double aY0, double aDx, double aDy, int aNx, int aNy)

// === 构造方法 ===
ZeroBoundFunc2(double aX0, double aY0, double aDx, double aDy, ColumnMatrix aData)

// === 求值 ===
double subs(double aX, double aY)                                        // 超出区间返回 0.0
int getINear(double aX)                                                  // x 索引 clamp 到 [0, Nx-1]
int getJNear(double aY)                                                  // y 索引 clamp 到 [0, Ny-1]

// === 零边界标记（IZeroBoundFunc2） ===
double zeroBoundNegX()                                                   // x 负向零边界位置：x0 - dx
double zeroBoundPosX()                                                   // x 正向零边界位置：x0 + Nx * dx
double zeroBoundNegY()                                                   // y 负向零边界位置：y0 - dy
double zeroBoundPosY()                                                   // y 正向零边界位置：y0 + Ny * dy

// === 工厂（子类实现） ===
protected ZeroBoundFunc2 newInstance_(double aX0, double aY0, double aDx, double aDy, ColumnMatrix aData)
```
