# PBCFunc2

> `jse.math.function.PBCFunc2`

**核心职能**：二维周期边界数值函数，`final class extends ColumnMatrixFunc2`。XY 两个方向各自独立循环绕回（Periodic Boundary Condition）。

```java
// === 静态工厂 ===
static PBCFunc2 zeros(double aX0, double aDx, int aN)                   // 正方形均匀网格
static PBCFunc2 zeros(double aX0, double aY0, double aDx, double aDy, int aNx, int aNy)

// === 构造方法 ===
PBCFunc2(double aX0, double aY0, double aDx, double aDy, ColumnMatrix aData)

// === 求值 ===
double subs(double aX, double aY)                                        // 索引模 Nx/Ny 循环绕回
int getINear(double aX)                                                  // 索引模 Nx 循环绕回
int getJNear(double aY)                                                  // 索引模 Ny 循环绕回

// === 工厂（子类实现） ===
protected PBCFunc2 newInstance_(double aX0, double aY0, double aDx, double aDy, ColumnMatrix aData)
```
