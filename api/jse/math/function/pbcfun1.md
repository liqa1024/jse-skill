# PBCFunc1

> `jse.math.function.PBCFunc1`

**核心职能**：一维周期边界数值函数，`final class extends VectorFunc1`。查询点超出定义域时循环绕回（Periodic Boundary Condition）。

```java
// === 静态工厂 ===
static PBCFunc1 zeros(double aX0, double aDx, int aNx)

// === 构造方法 ===
PBCFunc1(double aX0, double aDx, Vector aF)                              // 均匀网格
PBCFunc1(IVector aX, IVector aF)                                          // 插值型

// === 求值 ===
double subs(double aX)                                                   // 索引模 Nx 循环绕回
int getINear(double aX)                                                  // 索引模 Nx 循环绕回

// === 运算操作（周期修正） ===
VectorFunc1Operation operation()
// integral(false, true) — 只考虑右侧边界
// convolve/refConvolve/convolveFull/refConvolveFull 同理

// === 工厂（子类实现） ===
protected PBCFunc1 newInstance_(double aX0, double aDx, Vector aData)
```
