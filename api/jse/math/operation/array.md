# ARRAY

> `jse.math.operation.ARRAY`

**核心职能**：纯静态方法类。所有方法直接操作原始类型数组 + shift 偏移 + length 长度。方法命名模式与 `DATA` 镜像：`ebeXxx`=逐元素二元运算，`mapXxx`=逐元素标量运算，`2Dest`=输出到目标数组，`2This`=原地修改。`private` 构造器，静态工具类。

```java
// === 命名模式说明 ===
// ebe = element-by-element (逐元素二元: LHS arr op RHS arr)
// map = 逐元素一元 (arr op scalar)
// 2Dest = 结果写入目标数组 rDest
// 2This = 原地修改 rThis

// === boolean[] 逻辑运算 ===
static void ebeAnd/ebeOr/ebeXor2Dest(boolean[] aL,int sL, boolean[] aR,int sR, boolean[] rD,int sD, int len)
static void mapAnd/mapOr/mapXor2Dest(boolean[] aL,int sL, boolean rhs, boolean[] rD,int sD, int len)
static void ebeAnd/ebeOr/ebeXor2This(boolean[] rT,int sT, boolean[] aR,int sR, int len)
static void mapAnd/mapOr/mapXor2This(boolean[] rT,int sT, boolean rhs, int len)
static void not2Dest(boolean[] aD,int sD, boolean[] rD,int sD, int len) / not2This(boolean[] rT,int sT, int len)
static boolean allOfThis/anyOfThis(boolean[] aT,int sT, int len)
static int countOfThis(boolean[] aT,int sT, int len)

// === double[] 算术/比较/归约/累积/排序 ===
static void ebePlus/Minus/Multiply/Div/Mod2Dest/2This(double[]...)
static void mapPlus/Minus/LMinus/Multiply/Div/LDiv/Mod/LMod2Dest/2This(double[]...)
static void ebeCompare/mapCheck2Dest → boolean[] (Equal/Greater/GreaterOrEqual/Less/LessOrEqual)
static void mapAbs/Negative2Dest/2This(double[]...)
static double sumOfThis/meanOfThis/prodOfThis/maxOfThis/minOfThis(double[] aT,int sT, int len)
static double statOfThis(double[] aT,int sT, int len, DoubleBinaryOperator)
static void cumsum/cummean/cumprod/cummax/cummin/cumstat2Dest(double[] aT,int sT, double[] rD,int sD, int len)
static void reverse2Dest/2This / sort / biSort(double[]...)

// === int[] / long[] / float[] — 对应重载（同上模式） ===
// 提供 int/long/float 版本的 plus/minus/multiply/div/mod/sum/mean/prod/max/min/sort 等

// === complex (double[]×2) — 复数数组运算 ===
// 实虚部分离存储，提供 plus/minus/multiply/div/mapFill/assign/forEach/reverse2Dest/sum/mean/prod/cumsum/cummean/sort 等
```
