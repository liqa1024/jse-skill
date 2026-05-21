# NeighborListGetter

> `jse.atom.NeighborListGetter`

**核心职能**：`implements AutoCloseable`。基于 Neighbour Cell List 算法 O(N) 固定半径近邻搜索，不缓存列表，通过 `IDxyzIdxDo` lambda 访问。线程安全。package-private 构造器，通过 `AtomicParameterCalculator.nl_()` 内部获取。

```java
void close()

// forEach 邻域 — 按原子索引
void forEachNeighbor(int idx, double rMax, boolean half, boolean check, IDxyzIdxDo)
void forEachNeighbor(int idx, double rMax, boolean half, IDxyzIdxDo)
void forEachNeighbor(int idx, double rMax, IDxyzIdxDo)
// forEach 邻域 — 按空间位置
void forEachNeighbor(double x, double y, double z, double rMax, boolean check, IDxyzIdxDo)
void forEachNeighbor(double x, double y, double z, double rMax, IDxyzIdxDo)
void forEachNeighbor(IXYZ pos, double rMax, IDxyzIdxDo)

// forEach Nnn（指定近邻数量上限）
void forEachNeighbor(int idx, double rMax, int nnn, boolean half, IDxyzIdxDo)
void forEachNeighbor(int idx, double rMax, int nnn, IDxyzIdxDo)

// forEach MHT（曼哈顿距离版本，6 个重载）
void forEachNeighborMHT(int idx, double rMax, ...)  // 对应上述参数组合

// forEach Cell
void forEachCell(double rCell, IntConsumer)          // 遍历 cell 内原子
void forEachMirrorCell(double rCell, IXYZIdxDo)      // 遍历镜像 cell
```
