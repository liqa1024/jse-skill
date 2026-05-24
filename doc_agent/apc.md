# jse — 原子参量计算器 APC

APC 是 jse 的近邻列表核心类，并在近邻列表之上提供 RDF/SF、BOOP、固体检测等常用结构参量。

> **类引用**：`APC`=`jse.atom.APC`，`AtomicParameterCalculator`=`jse.atom.AtomicParameterCalculator`，`IntVector`=`jse.math.vector.IntVector`，`XYZ`=`jse.atom.XYZ`，`IFunc1`=`jse.math.function.IFunc1`，`IVector`=`jse.math.vector.IVector`，`ILogicalVector`=`jse.math.vector.ILogicalVector`

## 核心工作流

`APC.of(data)` 创建 `AtomicParameterCalculator` 实例，`APC.of(data, nthreads)` 指定线程数。APC 实现了 `AutoCloseable`，但内部资源会在 GC 时自动释放，因此 Groovy 脚本中**无需手动 close**。`withOf` 提供作用域内自动关闭并返回结果，适合一次性分析：

```groovy
def rdf = APC.withOf(data) { apc -> apc.calRDF() }
```

长脚本中同一结构多次分析时，复用同一 APC 实例，并可以通过 `setAtomXYZ`/`setAtomType` 更新坐标和种类来避免重新构建所有近邻列表：

```groovy
def apc = APC.of(data, 4)                        // 4 线程
apc.setAtomXYZ(0, 1.0d, 2.0d, 3.0d)              // 更新坐标
apc.setAtomType(5, 2)                             // 更新种类
```

## 近邻列表

`getNeighborList(idx, rMax, nnn)` 返回指定原子的近邻索引列表（`IntVector`）。可选 `nnn` 限制近邻数上限，适合固定配位数的场景；省略则返回截断半径内所有近邻：

```groovy
IntVector nbrs = apc.getNeighborList(0, 3.5d, 12) // atom 0，3.5 Å，最多 12 个
```

也支持任意空间点的近邻查询：

```groovy
IntVector nbrs = apc.getNeighborList(new XYZ(1, 2, 3), 3.5d, 12)
```

`getNeighborList` 只返回近邻索引。需要获取近邻的绝对坐标（自动处理 PBC 下的镜像原子）时用 `getFullNeighborList`，返回 `[x, y, z, idx]` 四个 `Vector`：

```groovy
def (xVec, yVec, zVec, idxVec) = apc.getFullNeighborList(0, 3.5d, 12)
// xVec[i], yVec[i], zVec[i] 为近邻 i 的绝对坐标，idxVec[i] 为其索引
```

## RDF / SF

径向分布函数 $g(r)$，基于近邻直方图（壳层原子计数归一化）：

$$
g(r) = \frac{V}{4\pi r^2 \Delta r\, N^2} \sum_i \sum_{j \neq i} \delta(r - r_{ij})
$$

```groovy
IFunc1 rdf = apc.calRDF(200, 5.0d)               // Δr = 5.0/200 Å
IFunc1 rdfAB = apc.calRDF_AB(1, 2, 200, 5.0d)    // type 1–2 偏 RDF
IFunc1 rdfG = apc.calRDF_G(200, 5.0d)             // 高斯展宽
```

结构因子 $S(q)$ 通过 Debye 散射公式直接求和：

$$
S(q) = \frac{1}{N} \sum_i \sum_j e^{-i\mathbf{q} \cdot \mathbf{r}_{ij}}
$$

`RDF2SF` / `SF2RDF` 通过傅里叶变换关系互转：

$$
S(q) = 1 + \rho \int [g(r) - 1]\, e^{-i\mathbf{q} \cdot \mathbf{r}} \, d\mathbf{r}
$$

```groovy
IFunc1 sf = apc.calSF(200, 5.0d)                // Δq = 5.0/200 Å⁻¹，密度自动获取
IFunc1 rdf2 = APC.RDF2SF(sf, apc.rho(), 200, 5.0d)  // 静态互转需显式传入密度
```

## BOOP / 固体检测

基于 Steinhardt 键取向序参量（PRB 28, 784, 1983）。$Q_{lm}(i)$ 为原子 $i$ 的近邻球谐平均，`calBOOP` 计算旋转不变量 $Q_l$，`calBOOP3` 计算三阶不变量 $\hat{W}_l$：

$$
Q_{lm}(i) = \frac{1}{N_{\mathrm{nbr}}} \sum_{j \in \mathrm{nbr}(i)} Y_{lm}(\theta_{ij}, \varphi_{ij})
$$

$$
Q_l(i) = \sqrt{\frac{4\pi}{2l+1} \sum_{m=-l}^{l} \bigl| Q_{lm}(i) \bigr|^2 }
\qquad
\hat{W}_l(i) = \sum_{m_1,m_2,m_3}
\begin{pmatrix} l & l & l \\ m_1 & m_2 & m_3 \end{pmatrix}
Q_{lm_1}(i)\, Q_{lm_2}(i)\, Q_{lm_3}(i)
$$

`calABOOP` 使用 Lechner-Dellago 平均（JCP 129, 114707, 2008）：

$$
\bar{Q}_{lm}(i) = \frac{1}{N_{\mathrm{nbr}} + 1} \Bigl[ Q_{lm}(i) + \sum_{j \in \mathrm{nbr}(i)} Q_{lm}(j) \Bigr]
$$

再以上式代入 $Q_l$ 得到 $\bar{Q}_l$：

```groovy
IVector q4 = apc.calBOOP(4, 3.5d, 12)            // l=4，近邻判据 3.5 Å，最多 12 近邻
IVector w6 = apc.calBOOP3(6, 3.5d, 12)
```

`calConnectRatioBOOP` 基于原始 Ackland-Jones 方法（JCP 127, 234504, 2007），计算 $S_{ij}$ 键序关联参数：

$$
S_{ij} = \frac{\sum_{m} Q_{lm}(i)\, Q_{lm}^{*}(j)}
                { \bigl| \mathbf{Q}_{l}(i) \bigr| \cdot
                  \bigl| \mathbf{Q}_{l}(j) \bigr| }
$$

`calConnectRatioABOOP` 则在 Ackland-Jones 之前先做 Lechner-Dellago 平均（Acta Mater. 2025, 121871），即输入 $\bar{Q}_{lm}$ 替代 $Q_{lm}$。

统计每个原子近邻中 $|S_{ij}| > \mathrm{threshold}$ 的占比（连接比例）：

```groovy
IVector ratio = apc.calConnectRatioBOOP(6, 0.7d, 3.5d, 12)
// l=6, threshold=0.7, rNearest=3.5 Å, nnn=12
```

## Voronoi 分析

Voronoi 分析通过 Groovy 静态扩展注入 APC，直接在 apc 实例上调用 `calVoronoi`：

```groovy
def vertices = apc.calVoronoi(3.5d)              // rCutOff=3.5 Å
vertices.setAreaThreshold(0.01d)                 // 配置阈值
int coordination = vertices[0].coordination()    // 某原子的配位数
```

返回 `ICalculator`（即 `List<IVertex>`），每个 `IVertex` 包含配位数、原子体积、空腔半径等。完整 API 查 `api/jsex/voronoi/`。
