# jse — 基本数学库

jse 提供了一套简单的数学库，用于方便桥接内部各种功能。

> **类引用**：`IVector`=`jse.math.vector.IVector`，`Vectors`=`jse.math.vector.Vectors`，`IMatrix`=`jse.math.matrix.IMatrix`，`Matrices`=`jse.math.matrix.Matrices`，`MathEX`=`jse.math.MathEX`，`IComplexDouble`=`jse.math.IComplexDouble`，`IComplexVector`=`jse.math.vector.IComplexVector`，`DoublePair`=`jse.code.collection.DoublePair`，`UT`=`jse.code.UT`

## 整体架构

```
Vectors                              ← 工厂入口，创建向量
    ↓ 返回
IVector                              ← 核心接口
    ├── 直接方法 + Groovy 运算符重载   ← 常用运算（算术、统计、[] 索引等）
    ├── subVec()                     ← 零拷贝子向量切片
    └── op()                         ← 运算器，不常用的高级运算

MathEX                               ← 扩展数学（常量 / Code / Func / Fast / Adv）
    └── static 方法，独立于向量

UT.Math                              ← 便捷门面，整理转发标量/向量数学操作
```

jse 中更加广泛地使用实数向量来保持简洁，且对其提供了通用接口 `IVector`，本文档对此重点介绍。矩阵 `IMatrix` 的差异在最后单独说明。

## 创建向量

`Vectors` 是创建向量的统一静态工厂。

```groovy
IVector v1 = Vectors.zeros(5)            // 全零
IVector v2 = Vectors.ones(5)             // 全 1
IVector v3 = Vectors.NaN(5)              // 全 NaN

// 从 Groovy 列表直接创建
IVector v4 = Vectors.from([1.0d, 2.0d, 3.0d])

// 等差数列 / 等比数列
IVector v5 = Vectors.linsequence(0.0d, 0.5d, 5)   // [0, 0.5, 1.0, 1.5, 2.0]
IVector v6 = Vectors.linspace(0.0d, 1.0d, 5)      // [0, 0.25, 0.5, 0.75, 1.0]
IVector v7 = Vectors.logspace(1.0d, 100.0d, 5)    // 对数等分 5 个点

// 从闭包创建
IVector v8 = Vectors.from(5) { i -> (double) (i * i) }  // [0, 1, 4, 9, 16]
```

> 实际使用中推荐优先通过 `UT.Math` 创建（见后文），`Vectors` 主要用于 `from` 从已有数据构造，以及需要时使用部分特有的接口。
>
> ⚠️ `linspace`/`logspace` 基于累加实现，端点可能存在浮点误差。

## 常用接口与运算符重载

### 维度与元素访问

Groovy 脚本优先使用 `v[i]` / `v[i] = x` 运算符重载。

```groovy
IVector v = Vectors.from([1.0d, 2.0d, 3.0d, 4.0d, 5.0d])

int n = v.size()                 // 5

// Groovy 推荐：[] 运算符重载
double x = v[0]                  // 读取
v[0] = 10.0d                     // 单元素写入
v[0..2] = [0.1d, 0.2d, 0.3d]    // 范围写入

// Java 风格（等价）
double y = v.get(0)
v.set(0, 10.0d)
```

### 算术运算符

标量和逐元素算术均支持 Groovy 运算符重载。

```groovy
IVector a = Vectors.from([1.0d, 2.0d, 3.0d])
IVector b = Vectors.from([4.0d, 5.0d, 6.0d])

// 标量运算
IVector c = a + 1.0d             // [2, 3, 4]
IVector d = a * 2.0d             // [2, 4, 6]

// 逐元素运算
IVector e = a + b                // [5, 7, 9]
IVector f = a * b                // [4, 10, 18]

// 一元
IVector g = a.abs()              // 逐元素绝对值
IVector h = -a                   // 取负
```

**原位运算**（`2this` 后缀，void，不创建新向量）：

```groovy
v.plus2this(1.0d)                // v 每个元素 += 1
v.multiply2this(otherVec)        // 每个 i: v[i] *= otherVec[i]
```

> ⚠️ **`v += 3.14d` 不等价于 `v.plus2this(3.14d)`** — Groovy 中 `v += x` 展开为 `v = v + x`，会创建新向量并重新赋值变量，原向量不变。需要原地修改时使用 `plus2this`。

#### 左侧运算

Groovy 默认不支持 `1.0d + v`（`Number` 没有 `plus(IVector)`）。`MathExtensions` 通过 Groovy `@Extension` 机制注入此能力：

```groovy
IVector v = Vectors.linsequence(1.0d, 1.0d, 3)   // [1, 2, 3]

IVector a = 1.0d + v              // [2, 3, 4]
IVector b = 2.0d * v              // [2, 4, 6]
IVector c = 10.0d - v             // [9, 8, 7]
IVector d = 12.0d / v             // [12, 6, 4]
```

### 统计与归约

```groovy
IVector v = Vectors.from([1.0d, 2.0d, 3.0d, 4.0d, 5.0d])

double s = v.sum()               // 15.0
double m = v.mean()              // 3.0
double p = v.prod()              // 120.0
double mx = v.max()              // 5.0
double mn = v.min()              // 1.0
```

### 批量操作

```groovy
v.fill(0.0d)                     // 全部置零
v.assign { -> Math.random() }    // 逐元素赋值
v.forEach { val -> println(val) } // 遍历
```

### 单元素原子操作

```groovy
v.increment(0)                   // v[0] += 1
v.decrement(0)                   // v[0] -= 1
v.add(0, 5.0d)                   // v[0] += 5
v.update(0) { x -> x * 2.0d }    // v[0] *= 2

double old = v.getAndIncrement(0) // 返回旧值，然后 += 1
```

## 切片

```groovy
IVector v = Vectors.from([1.0d, 2.0d, 3.0d, 4.0d, 5.0d])

// 子向量（零拷贝视图，共享底层数据）
IVector sub = v.subVec(1, 4)     // [2, 3, 4]

// 深拷贝
IVector c = v.copy()
```

## 运算器 `op()`

接口直接提供的方法覆盖了绝大多数常用运算。`op()` 是 `operation()` 的 `@VisibleForTesting` 简写别名（Groovy 脚本优先使用），返回 `IVectorOperation`，提供部分不常用的高级运算：

```groovy
IVector a = Vectors.from([1.0d, 2.0d, 3.0d])
IVector b = Vectors.from([4.0d, 5.0d, 6.0d])
IVector dest = a.copy()

// dot / norm（仅 op() 提供）
double d = a.op().dot(b)         // 点积 a · b → 32.0
double d2 = a.op().dot()         // 自身内积 → 14.0
double n = a.op().norm()         // L2 范数
double n1 = a.op().norm1()       // L1 范数

// 累积统计（仅 op() 提供）
IVector cs = a.op().cumsum()     // [1, 3, 6]
IVector cm = a.op().cummean()    // [1, 1.5, 2]

// 2dest：结果写入目标向量，既不创建新向量也不修改 this
a.op().div2dest(b, dest)         // dest = a / b

// l* 左变体：交换左右操作数
IVector r = a.op().ldiv(b)       // r = b / a（而非 a / b）
```

## IMatrix — 与 IVector 的差异

`IMatrix` 与 `IVector` 概念平行，通过 `Matrices` 工厂创建。以下仅列关键差异：

**不支持 `[][]` 索引**，必须使用 `get`/`set`：

```groovy
IMatrix m = Matrices.zeros(2, 3)
double x = m.get(0, 1)
m.set(0, 1, 5.0d)
// m[0][1]                       // ✗ 不支持
```

**维度与行列视图**：

```groovy
int nr = m.nrows()
int nc = m.ncols()
IVector row0 = m.row(0)          // 单行向量
IVector col1 = m.col(1)          // 单列向量
```

**Groovy 运算符**仅支持标量和矩阵间 `+` `-` `*` `/`，无逐元素比较、无 `[]` 重载。其余接口与 `IVector` 基本一致（`fill`、`2this` 原位、`op()` 等），`2this` 操作同理受 `+=` 不等价规则约束。

## MathEX — 扩展数学

`MathEX` 为静态工具类，提供数学常量；下文只介绍常用的 4 组静态内部类。

### 常量

```groovy
MathEX.PI            // 圆周率
MathEX.E             // 自然常数
MathEX.SQRT2         // √2
MathEX.SQRT3         // √3
MathEX.i1            // 虚数单位 (0+1i)
```

### MathEX.Code — 数值工具

```groovy
int i = MathEX.Code.floor2int(3.7d)       // 3
int j = MathEX.Code.ceil2int(3.2d)        // 4
long k = MathEX.Code.round(3.5d)          // 4

// 浮点比较（容差 DBL_EPSILON = 1e-10）
boolean eq = MathEX.Code.numericEqual(a, b)

// 范围钳制
double v = MathEX.Code.toRange(0.0d, 1.0d, 1.5d) // → 1.0

// 向上取整除法
long n = MathEX.Code.divup(10, 3)          // 4
```

### MathEX.Fast — 快速数学函数

委托 jafama `FastMath`，性能优于 `java.lang.Math`，精度略低。覆盖 `sqrt`/`exp`/`log`/`pow`/`sin`/`cos`/`tan` 及全部反双曲函数。

### MathEX.Func — 特殊函数

```groovy
// 球谐函数（复/实，单个/全 l）
IComplexDouble y = MathEX.Func.sphericalHarmonics(2, 1, theta, phi)
IComplexVector full = MathEX.Func.sphericalHarmonicsFull(4, theta, phi)
IVector realSH = MathEX.Func.realSphericalHarmonics(2, theta, phi)

// 连带 Legendre / Chebyshev 多项式
double P = MathEX.Func.legendre(2, 1, x)
double T = MathEX.Func.chebyshev(3, x)

// 线性插值
double yi = MathEX.Func.interp1(x1, x2, f1, f2, xq)

// 阶乘（返回 double 避免整型溢出）
double f = MathEX.Func.factorial(5)        // 120.0
```

### MathEX.Adv — 数值分析

```groovy
// 梯形数值积分
double I = MathEX.Adv.integral(0.0d, 1.0d, 100) { x -> x * x }

// 线性拟合
DoublePair ab = MathEX.Adv.lineFit(xVec, yVec)       // y = a + bx → {a, b}
double b = MathEX.Adv.lineFit0(xVec, yVec)           // y = bx（不含截距）
```

## UT.Math — 便捷门面

`UT.Math` 将标量数学函数广播到 `IVector` 的每个元素，是日常使用最便捷的入口。支持静态导入实现 matlab 风格调用：

```groovy
import static jse.code.UT.Math.*

IVector v = linspace(0.0d, PI, 5)

// 逐元素数学函数
IVector sv = sin(v)              // sin(v[i])
IVector ev = exp(v)              // exp(v[i])
IVector sq = sqrt(v)             // sqrt(v[i])
IVector pw = pow(v, 2.0d)        // pow(v[i], 2)

// 标量函数（底层委托 jafama FastMath）
double x = sqrt(2.0d)
double y = pow(2.0d, 10.0d)
```

`IMatrix` 版本命名和模式完全一致（如 `sqrt(m)` 对矩阵逐元素 sqrt）。

### 创建快捷方法

`zeros`/`ones`/`linspace`/`logspace`/`rand`/`randn` 统一通过 `UT.Math` 使用：

```groovy
import static jse.code.UT.Math.*

IVector v1 = zeros(5)
IVector v2 = ones(5)
IVector v3 = linspace(0.0d, 1.0d, 10)
IVector v4 = randn(100)          // 标准正态分布
IVector v5 = rand(100)           // [0,1) 均匀分布

IMatrix m1 = zeros(3, 4)
IMatrix m2 = randn(3, 4)
```

对于从已有数据创建（`from`），使用 `Vectors.from()` 工厂方法，或 `zeros` + `fill` 组合：

```groovy
IVector v = Vectors.from([1.0d, 2.0d, 3.0d])
// 或
IVector v = UT.Math.zeros(3)
v.fill([1.0d, 2.0d, 3.0d])
```

### 常量

```groovy
UT.Math.PI          // 圆周率（别名 pi）
UT.Math.E           // 自然常数（别名 e）
UT.Math.NaN         // NaN（别名 nan）
UT.Math.Inf         // 无穷大（别名 inf）
UT.Math.i1          // 虚数单位 0+1i（别名 j1）
```

## 使用 Tips

### 优先使用 Groovy 运算符

```groovy
// ✓ 推荐
IVector c = a + b
IVector d = v * 2.0d

// ✗ 不推荐（除非需要 Java 互操作）
IVector c = a.plus(b)
```

### 注意 `v += x` 不等价于原地修改

```groovy
v += 3.14d           // 创建新向量并重新赋值，原向量不变
v.plus2this(3.14d)   // 原地修改，不分配新向量
```

大数据量场景优先使用 `2this` 原位操作。

### `op()` 仅在需要高级运算时使用

`sum`/`mean`/`max`/`min`/`fill` 等大多数常用运算直接在 `IVector` 接口上可用。仅当需要 `dot`/`norm`/`cumsum`/`cummean`、`2dest`（写入目标向量）或 `l*` 左变体（交换操作数顺序）等高级运算时才使用 `op()`。

### 避免不必要的拷贝

| 操作 | 行为 |
|---|---|
| `v.subVec(from, to)` | 零拷贝视图，共享底层数据 |
| `v.xxx2this()` | 原地修改，不分配 |
| `v.copy()` | 显式深拷贝 |

### 创建方式选择

`zeros`/`ones`/`linspace`/`logspace`/`rand`/`randn` 统一使用 `UT.Math`。从已有列表/数组创建使用 `Vectors.from()`，或 `zeros` + `fill`。
