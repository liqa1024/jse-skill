# `jsex.voronoi`
> 3D 增量 Voronoi 图构造与几何分析——基于增量 flip 算法（参考 Hugo Ledoux 2006 和 Hellblazer/Voronoi-3D），使用鲁棒浮点几何谓词（Shewchuk 自适应精度）。提供 Voronoi 参数（配位数、原子体积、空腔半径、Voronoi Index）的实时计算，支持 PBC 镜像处理，并通过扩展方法注入 `AtomicParameterCalculator` 和 `MathEX.Graph`。

## 架构总览 (Architecture)

```
Geometry (static, 3rd-party: Colorado School of Mines) — 3D 鲁棒几何谓词

VoronoiBuilder (final)                          — 增量 3D Voronoi 构造器
  ├─ IVertex                                     — Voronoi 顶点接口（配位数/体积/空腔半径/VI）
  └─ ITetrahedron                                — Voronoi 四面体接口（外接球心/近邻）

VoronoiExtensions (static)                      — APC 扩展: calVoronoi → ICalculator
  └─ ICalculator extends List<IVertex>, RandomAccess

VoronoiStaticExtensions (static)                — MathEX.Graph 扩展: leftOfPlane/inSphere/centerSphere
```
