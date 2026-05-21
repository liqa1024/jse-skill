# Vectors

> `jse.math.vector.Vectors`

**核心职能**：创建各类向量的统一入口。涵盖 `zeros/ones/NaN`、从 `double[]`/`IVectorGetter`/`Iterable`/`Closure`/numpy 转换、`linspace`/`logspace` 序列生成、`range`、`merge`、`filter`。`final class`，私有构造函数，纯静态方法类。

```java
// === 默认 double 构造（返回 Vector） ===
static Vector zeros(int aSize)                               // 全零向量
static Vector ones(int aSize)                                // 全 1 向量
static Vector NaN(int aSize)                                 // 全 NaN 向量

// === 从已有数据拷贝 ===
// :note: Groovy 中列表直接匹配 Collection/Iterable 重载，无需 as double[] 强转
static Vector from(int aSize, IVectorGetter)                 // 从 getter
static Vector from(IVector) / fromDouble(IVector)            // 从已有向量拷贝
static Vector from(Iterable<? extends Number>)               // 从 Iterable
static Vector from(Collection<? extends Number>)             // 从 Collection（Groovy 首选）
static Vector from(double[] aData)                           // 从数组拷贝
static Vector from(int aSize, Closure<? extends Number>)     // Groovy 闭包

// === 从 numpy NDArray 创建（自动检测类型，零拷贝） ===
static Object fromNumpy(NDArray<?> aNDArray, boolean unsignedWarning)
static Object fromNumpy(NDArray<?> aNDArray)                 // unsignedWarning=true

// === 等差数列 / 等比数列 ===
static Vector linsequence(double start, double step, int n)  // start, start+step, start+2step, ...
// :note: linspace/logspace 基于累加实现，端点可能存在浮点误差
static Vector linspace(double start, double end, int n)      // 等分 n 个点
static Vector logsequence(double start, double step, int n)  // 对数步进
static Vector logspace(double start, double end, int n)      // 对数等分

// === Boolean 向量构造 ===
static LogicalVector fromBoolean(int size, ILogicalVectorGetter)
static LogicalVector fromBoolean(ILogicalVector/Iterable<Boolean>/Collection/boolean[]/Closure<Boolean>)

// === Int 向量构造 ===
static IntVector fromInt(int size, IIntVectorGetter)
static IntVector fromInt(IIntVector/Iterable<Integer>/Collection/int[]/Closure<Integer>)
static IntVector range(int size)                             // [0, 1, 2, ..., size-1]
static IntVector range(int start, int stop)                  // [start, ..., stop-1]
static IntVector range(int start, int stop, int step)

// === 向量拼接 ===
static Vector merge(IVector before, IVector after)
static LogicalVector merge(ILogicalVector, ILogicalVector)
static IntVector merge(IIntVector, IIntVector)
static ComplexVector merge(IComplexVector, IComplexVector)

// === 过滤 ===
static Vector filter(Iterable<? extends Number>, IDoubleFilter)
static Vector filter(IVector, IDoubleFilter)
```
