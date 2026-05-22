# jse — NumPy 互操作与线性代数

jse 数学容器（`IVector`/`IMatrix`/`ITable`）主要用于轻量数据组织、筛选、统计和脚本流程控制。线性代数不走 jse 内部矩阵运算，统一交给 NumPy/SciPy。本文关注 jse 与 NumPy 之间的数据转换路径、调用策略和边界条件。

> **类引用**：`SP.Python`=`jse.code.SP.Python`，`IVector`=`jse.math.vector.IVector`，`Vectors`=`jse.math.vector.Vectors`，`IMatrix`=`jse.math.matrix.IMatrix`，`Matrices`=`jse.math.matrix.Matrices`，`ITable`=`jse.math.table.ITable`

## 核心取向

jse 数学容器不是 NumPy 的替代品。`IVector`/`IMatrix` 提供的能力集中在元素访问，以及简单的算术、统计和视图切片——没有成熟的 matmul、eig、svd、lstsq 等线性代数方法，也不考虑重复扩展出这些能力。

当脚本需要线性代数时，策略是：**用 jse 容器组织输入 → 转为 NumPy → 在 Python 侧完成计算 → 当最终结果在 jse 侧有后续消费时转回**。

## 环境与边界

NumPy 互操作依赖 Jep/Python/JNI 环境，前置于 `python.md` 中描述的 Groovy↔Python 调用链。首次使用或新环境需确认 JNI 已构建：

```bash
jse --jnibuild
```

`SP.Python.NUMPY_SUPPORT` 可检测当前环境是否可用 NumPy。更多基本 Python 交互事项查看 `python.md`。

## 数据转换

jse 容器与 NumPy ndarray 之间的转换入口集中在各容器的 `.numpy()` 方法和工厂的 `.fromNumpy()` 静态方法。转换前注意查 `api/` 以确认具体签名、返回类型和支持范围——以下仅给出入口概览，不枚举所有重载。

### jse → NumPy

`.numpy()` 方法在 jse 侧返回 Jep 的 `NDArray` 包装对象。当此对象作为参数传入 Python 函数时，Jep 在跨语言边界将其转为 Python ndarray（值拷贝）。

```groovy
NDArray<double[]> nd = vec.numpy()       // IVector.numpy()，shift==0 时零拷贝底层数组
NDArray<double[]> nd = mat.numpy()       // IMatrix.numpy()
Map<String, NDArray<double[]>> m = table.numpy()  // 每列独立转为 NDArray，列名→数组映射
```

> jse 内部零拷贝仅当底层数组无偏移（`shift==0`）时成立。`RowMatrix`（行主序）天然满足；`ColumnMatrix` 的 `numpy()` 会复制。使用过 `subVec()` 或 `refSlicer()` 切片的向量/矩阵，`numpy()` 同样产生拷贝。

**支持 ndarray 转换的类型**：double / float / int / long / boolean。**complex vector/matrix 不支持**直接 `numpy()`，需通过 `.real()` / `.imag()` 分别取出后再转。

Python 侧接收后即为标准 ndarray，可直接投入 NumPy/SciPy 计算：

```python
def compute(arr):
    U, s, Vt = np.linalg.svd(arr, full_matrices=False)
    return U, s, Vt
```

### NumPy → jse

```groovy
def pyObj = SP.Python.get("some_ndarray")

// fromNumpy 自动检测 dtype 和 shape，零拷贝引用底层数组
def vec = Vectors.fromNumpy(pyObj)       // 一维 → Vector / IntVector / 等
def mat = Matrices.fromNumpy(pyObj)      // 二维 → RowMatrix / RowIntMatrix / 等
```

`fromNumpy` 返回 `Object`——实际类型取决于 ndarray 的 shape 和 dtype。**支持的 dtype**：`float64`→`Vector`、`float32`→`FloatVector`、`int32`→`IntVector`、`int64`→`LongVector`、`bool`→`LogicalVector`。不支持的 dtype（如 `complex64`/`complex128`、object、结构化 dtype）或 shape（三维及以上张量）会抛异常，由 Jep 或转换层直接报错，不会静默降级。

## 调用组织方式

Jep 在跨语言边界传输 ndarray 时总是值拷贝——即便 `numpy()` 在 jse 侧零拷贝，Jep 将 `NDArray` 转为 Python ndarray 仍然涉及整个数组的内存复制。Groovy→Jep→Python 的函数调用开销本身很小，**主要开销是每次传参时 ndarray 的值拷贝**。因此应避免在 Groovy 内反复调用 NumPy 函数。

推荐模式：把 NumPy/SciPy 计算封装在 Python 函数中，Groovy 只负责准备输入、发起一次较粗粒度的调用、取回最终必要结果：

```groovy
SP.Python.exec("""
import numpy as np

def decompose_and_project(matrix, vectors):
    U, s, Vt = np.linalg.svd(matrix, full_matrices=False)
    projections = [v @ U for v in vectors]
    return s, projections
""")

def calc = SP.Python.get("decompose_and_project")
def (s, projections) = calc(mat.numpy(), vecList*.numpy())
// s 为 Python ndarray 的 PyObject 引用
// projections 为 Python list of ndarray
```

> 复合返回值（tuple、list、dict 中嵌套 ndarray）不要假设可整体转回 jse。只有确认为一维/二维且 dtype 匹配 jse 支持类型的单一 ndarray 才适合走 `fromNumpy`。

## 线性代数策略与性能判断

决策线是复杂度：**O(N) 已有 jse 实现的走 jse；O(N²) 及以上、jse 未提供的走 NumPy/SciPy**。

### 建议走 jse

`dot`（内积）和 `norm`（范数）是 jse 已有且应优先使用的 O(N) 操作：

```groovy
double d = a.op().dot(b)     // ✓ jse 内积，O(N)，无跨语言开销，JIT 效果好
double n = a.op().norm()     // ✓ jse L2 范数

// ✗ 不要在 Groovy 侧为 dot/norm 引入 NumPy 往返
// np.dot(a.numpy(), b.numpy())  —— 多余的 Jep 传输和 Python 调用开销
```

逐元素算术、统计归约（`sum`/`mean`/`max` 等）同理——`IVector` 和 `UT.Math` 上已有完整实现（详见 `math.md`），不应绕到 NumPy。

### 建议走 NumPy/SciPy 的

以下操作 jse 未提供、算法复杂度 O(N²) 及以上，统一交给 Python 侧：

矩阵乘法（matmul，区别于内积 dot）、线性方程组求解、特征值/特征向量、SVD、最小二乘、Cholesky/QR/LU 分解、稀疏矩阵——这些走 `np.linalg` / `scipy.linalg` / `scipy.sparse`。具体 API 不在此展开，按任务查 NumPy/SciPy 文档。

### 性能判断

Groovy→Jep→Python 的调用开销本身很小。主要开销来自两处：**Jep 边界 ndarray 值拷贝**（每次传输复制整个数组），以及 **Python→NumPy→BLAS** 计算链路本身的开销。大规模 O(N³) 计算中两者均被摊销，但在以下场景会主导：

- **极小规模**（n < 50 的矩阵乘法或求解）：ndarray 拷贝和 NumPy/BLAS 初始化开销可能超过实际计算时间。如果调用在循环内且无法合并，审视是否真的需要线性代数
- **频繁的小规模往返**：循环内每次传 ndarray 都触发值拷贝，拷贝开销随循环次数线性累积

**写脚本前应判断**：
1. 是否真的需要线性代数——很多看似矩阵的问题可以用更简单的数据表达完成
2. 操作是否 jse 已有高效 O(N) 实现——`dot`/`norm`/逐元素运算 jse 已提供，无需引入 NumPy 依赖
3. 是否可以将多次小调用合并为一次粗粒度 Python 函数调用

## 边界与陷阱

核心原则：**可读性和一致性优先于微优化**。单次 ndarray 值拷贝通常不是瓶颈，代码碎片化（Groovy 和 Python 互相穿插调用）的维护成本远高于转换开销。

**代码一致性优先**。主要 Groovy 脚本中，Python 计算结果应当转回 jse 容器，使后续操作保持在 Groovy 语境中。jse 已有的操作（`dot`/`norm`/逐元素运算）不应为了一次调用绕到 NumPy，引入多余的 `numpy()` 往返和混合语言语境。

**外部语言语义最小化**。对于 Groovy 为主的脚本，Python 部分应是一个"计算块"：接收 ndarray → 完成线性代数 → 返回结果。不要让 Python 承担 I/O、数据整理、业务逻辑等计算之外的职责。即使 Python 侧能做，也不代表应该做。

**I/O 走 jse**。jse 有成熟的 `IO` 和各格式解析器，Python 侧也建议用 jse 读写——为此将结果转回 jse 容器是合理的转换开销。**绘图则更复杂，策略详见 `plot.md`**，在 math3 层面只需知道计算结果按需留在 Python 侧或转回 Groovy。

**客观限制**。以下无法绕过：复合返回值需逐一确认后才能 `fromNumpy`；复数、结构化 dtype、三维以上张量 jse 不支持直接转换，需分解后处理或留在 Python 侧。
