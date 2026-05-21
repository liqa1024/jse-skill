# `jse.math.vector`

> 61 个文件，6 种数据类型（double/float/int/long/boolean/complex），统一分层架构。**`Vectors` 为工厂入口**，独立于类型继承体系。

## 架构总览 (Architecture)

6 种类型共享同一六层模式。以 double 为例：`IVector`（接口）→ `AbstractVector`（骨架）→ `DoubleArrayVector`（数组层，实现 `IDataShell`）→ `Vector`（final 实现，`mShift` 零拷贝切片）。每种类型另有 `Operation`（运算分离，含 `2this`/`2dest`/`l*` 三变体 + `ARRAY` 数组优化路径）、`Slicer`（切片）、`Ref*Vector`（引用视图，`set` 默认抛异常）。

```
I{Type}Vector (接口)      I{Type}VectorOperation (运算接口)     I{Type}VectorSlicer (切片接口)
    ↑                             ↑                               ↑
Abstract{Type}Vector        Abstract{Type}VectorOperation       Abstract{Type}VectorSlicer
    ↑                             ↑
{Type}ArrayVector (IDataShell)    {Type}ArrayVectorOperation (ARRAY 直接数组优化, 否则 fallback DATA)
    ↑
{Type}Vector (具体实现, mShift+mSize+mData, subVec 零拷贝)    Ref{Type}Vector (引用视图)
```

**跨类型对比**

| 特性 | double | float | int | long | boolean | complex |
|---|---|---|---|---|---|---|
| **算术运算符** | plus/minus/multiply/div/mod (含 l*) | ❌ | plus/minus/multiply/div/mod | ❌ | ❌ | plus/minus/multiply/div + lminus/ldiv |
| **统计** | sum/mean/prod/max/min | ❌ | sum/exsum/mean/prod/max/min | sum/mean/prod/max/min | all/any/count | sum/mean/prod |
| **累积** | cumsum/cummean/cumprod/cummax/cummin | ❌ | ❌ | ❌ | cumall/cumany/cumcount | cumsum/cummean/cumprod |
| **逻辑运算** | ❌ | ❌ | ❌ | ❌ | and/or/xor/not | ❌ |
| **dot/norm** | dot/norm/norm1 | ❌ | ❌ | ❌ | ❌ | dot/norm |
| **比较** | equal/greater/less(OrEqual) | ❌ | ❌ | ❌ | ❌ | ❌ |
| **FMA** | mplus2this (double) | ❌ | ❌ | ❌ | ❌ | mplus2this (double/IComplexDouble) |
| **2dest 变体** | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **单元素原子操作** | increment/decrement/add/update | ❌ | increment/decrement/add/update | increment/decrement/add/update | flip | add/addImag/update/updateReal/updateImag |
| **numpy 转换** | `numpy()→NDArray<double[]>` (shift=0 零拷贝) | `numpy()→NDArray<float[]>` | `numpy()→NDArray<int[]>` | `numpy()→NDArray<long[]>` | `numpy()→NDArray<boolean[]>` | 无直接 numpy，通过 `real()/imag()→Vector` 间接转换 |
| **数组优化** | DoubleArrayVectorOp | FloatArrayVectorOp | IntArrayVectorOp | LongArrayVectorOp | BooleanArrayVectorOp | BiDoubleArrayVectorOp |
