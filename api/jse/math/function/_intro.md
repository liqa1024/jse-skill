# `jse.math.function`

> 33 个文件，一维/二维/三维数值函数体系。核心设计：边界策略（常值/零/周期/对称/固定）× 插值方式（等距/非等距）× 运算分离（Operation 模式，含 gradient/laplacian/integral/convolve）。

## 架构总览 (Architecture)

```
IFunc1Subs (@FunI) → IFunc1 → (IZeroBoundFunc1, IEqualIntervalFunc1)
    → AbstractFunc1 → VectorFunc1(IDataShell<Vector>) → ConstBound/ZeroBound/ZeroBoundSym/PBC/FixBound + UnequalIntervalFunc1
IFunc2Subs (@FunI) → IFunc2 → (IZeroBoundFunc2, IEqualIntervalFunc2)
    → AbstractFunc2 → ColumnMatrixFunc2(IDataShell<ColumnMatrix>) → ConstBound/ZeroBound/ZeroBoundSym/PBC
IFunc3Subs (@FunI) → IFunc3 → IEqualIntervalFunc3 (@Experimental, 无骨架/运算器)

IFunc1Operation → AbstractFunc1Operation → VectorFunc1Operation (同网格→Vector批量运算)
IFunc2Operation → AbstractFunc2Operation → ColumnMatrixFunc2Operation (同网格→ColumnMatrix批量运算)
```

**Func1/Func2** 为静态工厂入口，独立于上述继承体系。

### 边界行为速查

| 类 | 超左界 | 超右界 | 特殊 |
|---|---|---|---|
| `ConstBoundFunc1` | clamp→端点值 | clamp→端点值 | 默认实现 |
| `ZeroBoundFunc1` | 0.0 | 0.0 | 每侧多扩展一个 dx |
| `ZeroBoundSymmetryFunc1` | 镜像至正侧 | 0.0 | 关于 x0 对称，范围 2Nx |
| `PBCFunc1` | 周期折回 | 周期折回 | do...while 循环 |
| `FixBoundFunc1` | mBoundL | mBoundR | 用户自定义 |
| `UnequalIntervalFunc1` | mF[0] | mF[Nx-1] | 二分查找+线性插值 |
