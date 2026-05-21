# ZeroBoundSymmetryFunc1

> `jse.math.function.ZeroBoundSymmetryFunc1`

**核心职能**：一维零边界对称数值函数，`final class extends VectorFunc1 implements IZeroBoundFunc1`。以 `x0` 为轴镜像对称，超出对称范围后返回 `0.0`。

```java
// === 静态工厂 ===
static ZeroBoundSymmetryFunc1 zeros(double aX0, double aDx, int aNx)

// === 构造方法 ===
ZeroBoundSymmetryFunc1(double aX0, double aDx, Vector aF)               // 均匀网格
ZeroBoundSymmetryFunc1(IVector aX, IVector aF)                           // 插值型

// === 求值 ===
double subs(double aX)                                                   // 负侧镜像映射，超出对称域返回 0.0
int getINear(double aX)                                                  // 负侧镜像映射后 clamp 到 [0, Nx-1]

// === 零边界标记（IZeroBoundFunc1） ===
double zeroBoundL()                                                      // 左侧零边界位置：x0 - Nx * dx
double zeroBoundR()                                                      // 右侧零边界位置：x0 + Nx * dx

// === 运算操作（对称修正） ===
VectorFunc1Operation operation()
// Laplacian 保持对称性；积分结果 ×2；卷积结果 ×2

// === 工厂（子类实现） ===
protected ZeroBoundSymmetryFunc1 newInstance_(double aX0, double aDx, Vector aData)
```
