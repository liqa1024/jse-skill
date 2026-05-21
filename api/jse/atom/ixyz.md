# IXYZ

> `jse.atom.IXYZ`

**核心职能**：定义三维空间坐标的只读协议，并提供全套向量算术运算（61 个 default 方法）。是整个 atom 包的基石接口。无基底接口。

```java
// === 抽象方法（子类必须实现） ===
double x()                     // x 坐标值
double y()                     // y 坐标值
double z()                     // z 坐标值

// === 只读向量运算（全部返回新建对象） ===
IXYZ copy()                    // 深拷贝，默认返回 new XYZ(this)
Vector toVec()                  // 转为数学 Vector
NDArray<double[]> numpy()      // numpy 数组（值拷贝）
double[] data()                 // 兼容 double[]{x,y,z}（值拷贝）

// 统计
double sum()                   // x + y + z
double mean()                  // (x + y + z) / 3
double prod()                  // x * y * z
double min() / max()           // min(x,y,z) / max(x,y,z)

// 向量运算
double dot()                   // 自点积 x²+y²+z²
double dot(IXYZ/XYZ/double,double,double)   // 点积
XYZ cross(IXYZ/XYZ/double,double,double)    // 叉积（返回 XYZ）
double mixed(IXYZ+IXYZ / XYZ+XYZ / 9 double) // 混合积标量
double norm()                  // L2 范数 sqrt(dot())
double norm1()                 // L1 范数 |x|+|y|+|z|
XYZ negative()                 // 取反 (-x, -y, -z)
XYZ abs()                      // 逐分量绝对值

// 加减乘除（3 参数重载族: IXYZ / XYZ / 3个double）
XYZ plus(IXYZ/XYZ/double,double,double)     // this + rhs
XYZ minus(IXYZ/XYZ/double,double,double)    // this - rhs
XYZ lminus(IXYZ/XYZ/double,double,double)   // rhs - this（左减法）
XYZ multiply(IXYZ/XYZ/double,double,double) // 逐分量乘
XYZ div(IXYZ/XYZ/double,double,double)      // 逐分量除
XYZ ldiv(IXYZ/XYZ/double,double,double)     // rhs / this（左除法）
XYZ plus/minus/multiply/div(double)          // 标量运算

// 距离
double distance2(IXYZ/XYZ/double,double,double)    // 距离平方
double distance(IXYZ/XYZ/double,double,double)     // 欧几里得距离
double distanceQuick(IXYZ/XYZ/double,double,double)// 快速近似距离
double distanceMHT(IXYZ/XYZ/double,double,double)  // 曼哈顿距离
boolean numericEqual(IXYZ/XYZ/double,double,double)// 数值相等（容差比较）
```
