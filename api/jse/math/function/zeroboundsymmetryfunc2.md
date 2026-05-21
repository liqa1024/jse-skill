# ZeroBoundSymmetryFunc2

> `jse.math.function.ZeroBoundSymmetryFunc2`

**核心职能**：二维零边界对称数值函数，`final class extends ColumnMatrixFunc2 implements IZeroBoundFunc2`。以 `(x0, y0)` 为轴镜像对称，超出对称范围后返回 `0.0`。

```java
// === 静态工厂 ===
static ZeroBoundSymmetryFunc2 zeros(double aX0, double aDx, int aN)     // 正方形均匀网格
static ZeroBoundSymmetryFunc2 zeros(double aX0, double aY0, double aDx, double aDy, int aNx, int aNy)

// === 构造方法 ===
ZeroBoundSymmetryFunc2(double aX0, double aY0, double aDx, double aDy, ColumnMatrix aData)

// === 求值 ===
double subs(double aX, double aY)                                        // 双线性插值，负侧镜像映射，超出对称域返回 0.0
int getINear(double aX)                                                  // 负侧镜像映射后 clamp 到 [0, Nx-1]
int getJNear(double aY)                                                  // 负侧镜像映射后 clamp 到 [0, Ny-1]

// === 零边界标记（IZeroBoundFunc2） ===
double zeroBoundNegX()                                                   // x 负向零边界位置：x0 - Nx * dx
double zeroBoundPosX()                                                   // x 正向零边界位置：x0 + Nx * dx
double zeroBoundNegY()                                                   // y 负向零边界位置：y0 - Ny * dy
double zeroBoundPosY()                                                   // y 正向零边界位置：y0 + Ny * dy

// === 工厂（子类实现） ===
protected ZeroBoundSymmetryFunc2 newInstance_(double aX0, double aY0, double aDx, double aDy, ColumnMatrix aData)
```
