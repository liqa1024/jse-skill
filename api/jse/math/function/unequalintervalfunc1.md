# UnequalIntervalFunc1

> `jse.math.function.UnequalIntervalFunc1`

> 此类标记为 `@ApiStatus.Experimental`

**核心职能**：一维非均匀间隔数值函数，`final class extends AbstractFunc1`。内部存储 x 坐标数组 `mX[]` 和值数组 `mF[]`，使用 `Arrays.binarySearch` 二分查找定位区间。超出边界时返回最近端点值（零边界外推）。

```java
// === 静态工厂 ===
static UnequalIntervalFunc1 zeros(int aNx, IVectorGetter aXGetter)       // 通过 getter 生成递增 x 坐标

// === 构造方法 ===
UnequalIntervalFunc1(double[] aX, double[] aF)                           // 直接指定 x 和 f 数组
UnequalIntervalFunc1(double aX0, double aDx, double[] aData)             // 等间距输入，内部展开为 x 数组

// === 访问 x / f ===
IVector x()                                                              // 返回 mX 的只读 RefVector 视图
IVector f()                                                              // 返回 mF 的 Vector 副本
double getX(int aI)                                                      // 第 aI 个 x 坐标（带界检）
double x0()                                                              // 首个 x 坐标：mX[0]

// === 属性 ===
int Nx()                                                                 // 数据点数：mF.length
double dx(int aI)                                                        // 非均匀间距：mX[aI+1] - mX[aI]（带界检，适用 aI ∈ [0, Nx-2]）

// === 求值 ===
double subs(double aX)                                                   // 二分查找 + 线性插值，超出返回端点值
double get(int aI)                                                       // 按索引取值（带界检）
int getINear(double aX)                                                  // 二分查找最近索引

// === 修改 ===
void set(int aI, double aV)                                              // 按索引设值（带界检）
void setX0(double aNewX0)                                                // 整体平移 x 坐标
void fill(double[] aData)                                                // 批量覆盖 mF
void update(int aI, DoubleUnaryOperator aOpt)                            // 单元素更新
double getAndUpdate(int aI, DoubleUnaryOperator aOpt)                    // 取值并更新

// === 克隆与运算 ===
UnequalIntervalFunc1 copy()
IFunc1Operation operation()
```
