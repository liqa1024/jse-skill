# VoronoiBuilder

> `jsex.voronoi.VoronoiBuilder`

**核心职能**：`final` 类，基于增量 flip 算法（2→3 flip / 3→2 flip / 1→4 flip）维护 Delaunay 四面体剖分（Voronoi 的对偶）。从初始超大四面体开始，逐点 `insert` 并局部 flip 恢复 Delaunay 条件。提供 `IVertex`/`ITetrahedron` 接口访问 Voronoi 参数（配位数、原子体积、空腔半径、Voronoi Index），支持面积/边长截断阈值处理退化面。

```java
// === 构造 ===
VoronoiBuilder()                                // 使用全局随机数生成器
VoronoiBuilder(long aSeed)                      // 指定随机种子

// === 插入点 ===
void insert(IXYZ aXYZ)                          // 插入坐标点
void insert(double aX, double aY, double aZ)
void insert(IXYZ aXYZ, int atomIndex)           // 带原子索引（用于结果回查）
void insert(double aX, double aY, double aZ, int atomIndex)

// === 阈值配置（链式调用） ===
VoronoiBuilder setNoWarning(boolean aNoWarning) // 关闭退化警告
VoronoiBuilder setNoWarning()
VoronoiBuilder setAreaThreshold(double aAreaThreshold)       // 面积截断（相对总表面积）
VoronoiBuilder setLengthThreshold(double aLengthThreshold)   // 边长截断（相对原子间距）
VoronoiBuilder setAreaThresholdAbs(double aAreaThresholdAbs) // 面积截断（绝对值）
VoronoiBuilder setLengthThresholdAbs(double aLengthThresholdAbs) // 边长截断（绝对值）
VoronoiBuilder setIndexLength(int aIndexLength) // Voronoi Index 存储长度, 默认 9

// === 顶点访问 ===
IVertex getVertex(int aIdx)                     // 按插入顺序获取顶点
int sizeVertex()                                // 顶点数量
@Unmodifiable List<IVertex> allVertex()         // 全部顶点（只读视图）

// === 四面体访问 ===
ITetrahedron getTetrahedron()                   // 最近创建的四面体
@Unmodifiable Collection<ITetrahedron> allTetrahedron() // 全部四面体（只读视图）

// === 内部接口 ===
interface IVertex extends IXYZ {
    int coordination()                          // 配位数（经面积阈值截断）
    double atomicVolume()                       // 原子体积（棱锥法求和）
    double cavityRadius()                       // 空腔半径（到外接球心最大距离）
    int[] index()                               // Voronoi Index (长度为 mIndexLength)
    int atomIndex()                             // 原始原子索引
    double x() / double y() / double z()
    @Unmodifiable Collection<IVertex> neighborVertex()
    @Unmodifiable Collection<ITetrahedron> neighborTetrahedron()
}
interface ITetrahedron {
    IXYZ centerSphere()                         // 外接球心
    @Unmodifiable List<IVertex> neighborVertex()
    @Unmodifiable List<ITetrahedron> neighborTetrahedron()
    boolean valid()                             // 是否未被删除
}
```
