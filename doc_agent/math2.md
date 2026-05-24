# jse — 进阶数学库设计

`math.md` 已介绍最常用的 double 向量、矩阵和基础数学工具。本文从 jse 的实际支持重心补充进阶数学结构。

> **类引用**：`IVector`=`jse.math.vector.IVector`，`IIntVector`=`jse.math.vector.IIntVector`，`ILogicalVector`=`jse.math.vector.ILogicalVector`，`ILongVector`=`jse.math.vector.ILongVector`，`IFloatVector`=`jse.math.vector.IFloatVector`，`Vector`=`jse.math.vector.Vector`，`IntVector`=`jse.math.vector.IntVector`，`LongVector`=`jse.math.vector.LongVector`，`FloatVector`=`jse.math.vector.FloatVector`，`Vectors`=`jse.math.vector.Vectors`，`DoubleList`=`jse.code.collection.DoubleList`，`IntList`=`jse.code.collection.IntList`，`IDataShell`=`jse.math.IDataShell`，`IMatrix`=`jse.math.matrix.IMatrix`，`IIntMatrix`=`jse.math.matrix.IIntMatrix`，`ILogicalMatrix`=`jse.math.matrix.ILogicalMatrix`，`RowMatrix`=`jse.math.matrix.RowMatrix`，`Matrices`=`jse.math.matrix.Matrices`，`ITable`=`jse.math.table.ITable`，`Tables`=`jse.math.table.Tables`，`IFunc1`=`jse.math.function.IFunc1`，`Func1`=`jse.math.function.Func1`，`IFunc2`=`jse.math.function.IFunc2`，`Func2`=`jse.math.function.Func2`，`IComplexDouble`=`jse.math.IComplexDouble`，`ComplexDouble`=`jse.math.ComplexDouble`

## 核心取向

jse 数学库首先服务模拟数据处理中的简单数值容器，而不是复刻 NumPy / SciPy 的统一数组模型。最完整、最常用的主线是 `IVector`：大量内部数据都可以自然表示为一维序列，向量上的脚本操作、统计、筛选和原位修改也最充分。

因此，理解 jse 数学库时先从“这是不是一个向量问题”开始，而不是先寻找通用 ndarray、dtype 或线性代数框架。矩阵、表格、函数和复数都存在，但它们是围绕具体数据语义补充出来的结构。

## 特化向量

`IVector` 是 double 主线。特化向量不是 `IVector<T>`，也不是统一 dtype 参数，而是各自独立的接口族；支持能力不保证对称。向量构造完成后尺寸固定，需要不同长度时重新构造；如果长度在构造过程中逐步增长，用具体类的 `builder()` 收集元素后一次 `build()` 成固定尺寸向量。

```groovy
def b = Vector.builder()
b << 1.0d
b << 2.0d
IVector v = b.build()
```

### IIntVector

`IIntVector` 是支持度最高、实际使用最频繁的特化向量，适合类型编号、索引、计数、离散标签等整数数据。它保留了较完整的整数算术、统计、排序和随机打乱能力。

```groovy
IIntVector ids = Vectors.range(5)          // [0, 1, 2, 3, 4]
ids.add(0, 10)

int s = ids.sum()
long safe = ids.op().exsum()               // 扩展精度求和
IVector asDouble = ids.asVec()
```

`IIntVector` 还继承 `ISlice`，可直接作为 jse 向量切片输入。若要作为普通 Groovy/Java 列表索引使用，则用 `asList()` 获取列表视图。

```groovy
IVector x = Vectors.from([10.0d, 20.0d, 30.0d])
IIntVector pick = Vectors.fromInt([0, 2])

IVector y = x[pick]                       // jse 切片
List<Integer> idx = pick.asList()         // 一般 Groovy/Java 场景
```

注意按照 jse 约定，`asVec()` & `asList()` 返回引用视图而不是值拷贝。

### ILogicalVector

`ILogicalVector` 表示布尔掩码和条件结果。它不是数值向量的简化版，而有自己的逻辑运算、`all`/`any`/`count` 和 `where()` 索引提取。

```groovy
IVector x = Vectors.from([1.0d, -2.0d, 3.0d])
ILogicalVector mask = x.greater(0.0d)

boolean ok = mask.any()
int n = mask.count()
IVector positive = x[mask]                 // 按条件过滤
IIntVector where = mask.where()            // 获取位置索引
```

### ILongVector

`ILongVector` 适合长整数、大计数或需要保留 long 范围的数据。它的结构与 int 向量相近，但支持面更窄：没有直接的 plus/minus 等算术运算符，主要提供单元素更新、统计、排序和转换。

```groovy
ILongVector counts = LongVector.zeros(3)
counts.increment(0)

long total = counts.sum()
IVector asDouble = counts.asVec()
```

如果从一开始就需要大量向量化算术运算，应直接使用 double 的 `Vector` 存储；如果只是保存大整数计数、偶尔统计，或循环逻辑比向量语法更清楚，则保持 `ILongVector` 语义更合适。

### IFloatVector

`IFloatVector` 是轻量 float 存储，支持度最低。它主要用于节省存储或与外部 float 数据对接，不提供 double 向量那套完整算术和统计能力。

```groovy
IFloatVector fv = FloatVector.zeros(3)
fv.fill(1.0f)

IVector v = fv.asVec()                     // 获取 double 引用
```

一般脚本计算不应主动追求 float；除非数据来源或内存压力确实要求，否则使用 `IVector` 更直接。

### 可变长度与 native 输入

jse 中向量长度固定不变，对于需要可变长度的情况，可以使用对应的 `DoubleList`、`IntList` 等非装箱的动态 List。Builder 适合“构造一个向量”的场景，而这些则更适合本身长度就不确定的情况。

```groovy
DoubleList dl = new DoubleList()
dl << 1.0d
dl << 2.0d
assert dl.size() == 2
// 同样支持读取和写入
double x = dl[0]
dl[0] = 10.0d
```

`DoubleList` 和 `Vector` 都实现 `IDataShell<double[]>`，`IntList` 和 `IntVector` 都实现 `IDataShell<int[]>`，long/float/boolean 体系也遵循同一思路。因此很多以 `IDataShell` 为参数的 native 接口（C 指针，MPI 等）可以直接接收这些。

## 矩阵

`IMatrix` 可以理解为二维 double 数据结构，但它不是 jse 数学库的主线。实践中矩阵出现得比向量少得多：许多看似二维的数据在 jse 中会有更自然的对象模型，例如原子坐标通常使用 `List<XYZ>` / 原子结构类，而不是裸 `n×3` 矩阵。

矩阵构造完成后行列数固定，需要改变尺寸时重新构造。与向量相比，矩阵接口更克制；复杂操作更多放在 `op()` 中，日常代码只在确实需要二维结构时使用矩阵。

```groovy
IMatrix block = Matrices.zeros(3, 3)        // 小型数值块
block.set(0, 0, 1.0d)

int n = block.nrows()
IVector firstCol = block.col(0)
```

矩阵 Builder 与向量 Builder 不同：它会固定一侧维度，然后逐行或逐列追加。`RowMatrix.builder(ncols)` 逐行追加，`ColumnMatrix.builder(nrows)` 逐列追加。

```groovy
def mb = RowMatrix.builder(3)
mb.addRow(Vectors.from([1.0d, 2.0d, 3.0d]))
mb.addRow(Vectors.from([4.0d, 5.0d, 6.0d]))
IMatrix rows = mb.build()
```

特化矩阵大体延续向量思路，但支持更有限。`IIntMatrix` / `ILogicalMatrix` 主要保存整数或布尔二维数据，通常没有 double 矩阵的完整算术能力。

```groovy
IIntMatrix im = Matrices.fromInt(2, 2) { int i, int j -> i + j }
IMatrix dm = im.asMat()

ILogicalMatrix lm = Matrices.fromBoolean(2, 2) { int i, int j -> i == j }
IIntMatrix asInt = lm.asIntMat()
```

`RowMatrix` / `ColumnMatrix` 体现存储方向。通常只需通过 `Matrices` 构造；只有在行列访问性能或底层视图语义重要时才关心具体实现。

## Table

`ITable` 是带列名语义的二维数值数据。它不是普通矩阵的替代品：当列名本身有意义时，应保留表格结构；当只剩纯数值计算时，再通过 `asMatrix()` 进入矩阵。

表格构造后行数固定。列可以通过列赋值新增或替换，但应把它理解为结构化列数据，而不是任意动态 DataFrame。表格没有独立 Builder；构造期已有行/列数据时优先使用 `Tables.fromRows(...)` 或 `Tables.fromCols(...)`，再用列名运算符补充列。

```groovy
ITable t = Tables.fromCols([
    [0.0d, 1.0d, 2.0d],
    [10.0d, 11.0d, 13.0d],
], "time", "energy")

t["temp"] = [300.0d, 305.0d, 310.0d]

double e = t["energy"][1]
IMatrix raw = t.asMatrix()
```

CSV-like 数据、多列物理量、统计结果表通常比裸矩阵更适合用 `ITable` 表达；否则列的含义很容易在后续计算中丢失。`t["col"]` / `t["col"] = values` 分别映射到底层 `get` / `put`，Groovy 脚本中优先使用运算符写法。

## Func1

`IFunc1` 表示“数值序列 + x 坐标 + 边界策略”。它不是更高级的向量；只有当坐标、插值、边界行为或分布构造本身重要时才使用。

实践中最常用的是用工厂方法快速得到一维分布：

```groovy
IVector data = Vectors.from([1.0d, 2.0d, 2.5d, 4.0d])

IFunc1 hist = Func1.distFrom(data, 0.0d, 10.0d, 100)
IFunc1 smooth = Func1.distFrom_G(data, 0.0d, 10.0d, 100)
IFunc1 delta = Func1.deltaG(0.1d, 0.0d, 4.0d)
```

`Func1.from(...)`、插值、微分、积分、卷积等能力存在，但使用频率明显低于分布构造。若数据只是普通序列，用 `IVector` 更合适；只有 x 坐标和边界策略是问题的一部分时，才进入 `IFunc1`。

## Func2

`IFunc2` 是“二维矩阵 + x/y 坐标 + 边界策略”。它的使用频率和支持程度都低于 `IFunc1`，通常只在二维分布或网格函数场景中出现。

```groovy
IVector dx = Vectors.from([0.1d, 0.2d, 0.3d])
IVector dy = Vectors.from([0.4d, 0.5d, 0.6d])

IFunc2 hist2 = Func2.distFrom(dx, dy, 0.0d, 0.0d, 1.0d, 1.0d, 50, 50)
IFunc2 smooth2 = Func2.distFrom_G(dx, dy, 0.0d, 0.0d, 1.0d, 1.0d, 50, 50)
IFunc2 delta2 = Func2.deltaG(0.1d, 0.0d, 4.0d)
```

如果只是二维数值数据，优先使用 `IMatrix`；如果二维数据同时需要 x/y 坐标、插值或边界策略，才考虑 `IFunc2`。

## Complex

复数体系使用频率很低，且不是 double 向量/矩阵的 dtype 变体。`IComplexDouble` / `ComplexDouble` 表示单个复数，complex vector/matrix 是独立接口族。

```groovy
IComplexDouble z = new ComplexDouble(1.0d, 2.0d)
double r = z.real()
double im = z.imag()
```

遇到复数数据时，不要假设普通 `IVector` / `IMatrix` 方法可以直接套用；应查对应 complex API。
