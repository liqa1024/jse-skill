# MathEX.Code

> `jse.math.MathEX.Code`

**核心职能**：取整转换、范围钳制、浮点比较（含容差）、向上取整除法、2的幂次边界、单位换算。

```java
// 取整
static double floor/ceil(double) / long round(double)
static int floor2int/ceil2int/round2int(double)          // 转 int

// 范围钳制
static double/int/long toRange(double/int/long min, double/int/long max, double/int/long value)

// 浮点比较（基于 DBL_EPSILON=1.0e-10 的容差比较）
static boolean numericEqual(double a, double b)
static boolean numericGreater(double a, double b)         // a > b
static boolean numericLess(double a, double b)            // a < b
static final int EPS_MUL = 8
static final double DBL_EPSILON = 1.0e-10

// 向上取整除法
static long/int divup(long/int aNumber, long/int aDivider)

// 2 的幂次边界
static int ceilPower2(int) / floorPower2(int)
static int ceilPower(int, double root) / floorPower(int, double root)  // 任意幂次

// 单位换算
static long/int units(long/int amount, long/int originalUnit, long/int targetUnit, boolean roundUp)
```
