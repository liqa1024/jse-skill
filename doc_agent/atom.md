# jse — 原子结构基础

本文覆盖 jse 内存中的原子结构模型：坐标、原子、模拟盒、原子数据容器，以及最基础的构造和变换。文件格式读写、势函数、结构分析、ASE/LAMMPS 集成转到后续专题。

> **类引用**：`IAtomData`=`jse.atom.IAtomData`，`ISettableAtomData`=`jse.atom.ISettableAtomData`，`AtomData`=`jse.atom.AtomData`，`SettableAtomData`=`jse.atom.SettableAtomData`，`IXYZ`=`jse.atom.IXYZ`，`XYZ`=`jse.atom.XYZ`，`ISettableXYZ`=`jse.atom.ISettableXYZ`，`IAtom`=`jse.atom.IAtom`，`ISettableAtom`=`jse.atom.ISettableAtom`，`Atom`=`jse.atom.Atom`，`AtomID`=`jse.atom.AtomID`，`AtomFull`=`jse.atom.AtomFull`，`IBox`=`jse.atom.IBox`，`Box`=`jse.atom.Box`，`BoxPrism`=`jse.atom.BoxPrism`，`Structures`=`jse.atom.Structures`，`IAtomDataOperation`=`jse.atom.IAtomDataOperation`，`ISettableAtomDataOperation`=`jse.atom.ISettableAtomDataOperation`，`CS`=`jse.code.CS`

## 整体架构

```
IBox, IAtom, IAtomDataOperation
    ↓ 组合
IAtomData                             ← 核心入口，组合坐标/种类/盒/操作
    ├── atom(idx) / atoms()           ← 原子访问（IAtom）
    ├── box() / ntypes() / hasID()... ← 元数据
    └── op()                          ← 结构变换运算器

IXYZ → IAtom → ISettableAtom          ← 坐标→原子
     → IBox                           ← 坐标→模拟盒
```

jse 的原子结构不是裸坐标矩阵，而是一个以 `IAtomData` 为统一入口的复合模型。它把以下几个维度组织在一起：

- **原子坐标与属性** — 每个原子有 x/y/z 坐标和 type 种类编号，可选携带 id、速度、符号、质量
- **模拟盒** — `IBox` 描述正交或三斜
- **种类信息** — 种类数、元素符号映射、质量
- **结构级操作** — 通过 `op()` 获取运算器，提供过滤、切片、扩胞、PBC 绕回、团簇分析等

脚本中遇到原子体系，优先把它装进 `IAtomData`，而不是自己维护多列数组。文件读取、晶格构造、结构变换的入口都围绕这一模型展开。

## jse 原子结构约定

设计上尽可能忠实原始数据，同时通过 `IAtomData` 抽象统一访问行为：

- **访问时坐标统一为笛卡尔坐标**
- **访问时原子统一放在从原点开始的模拟盒内** — 带下边界的外部格式（如 LAMMPS data）访问时自动减去下边界，脚本中获取的坐标不会为负
- **写入过程逆处理** — 任何写入修改过程会做逆变换恢复原格式
- **不做单位转换** — 保留文件读入数据的原始数值

> 注意没有说明时上述访问和写入都为内存操作，jse 的文件读写完全保留原始数值不进行变换。

其余约定：

- `type` 从 **1** 开始，因此 `atom(i).type() <= data.ntypes()`
- `id` 不是多数结构的核心。部分格式不含真实 id，此时以 `index() + 1` 兜底。判断是否有真实 id 须看 `hasID()`
- 原子索引 `index()` 与原子 id 是两回事 — 前者是原子在容器中的位置，后者是外部格式中的标识号
- 更细的约定以 `_src/jse/atom/IAtomData.java` 类注释以及实际行为为准

## 坐标、原子与模拟盒

三者共享 `IXYZ` 作为统一的坐标语言，向不同方向延伸：

- **`IXYZ` / `XYZ`** — 纯三维坐标，承担通用的小型向量运算（距离、叉积、点积等，支持 Groovy 运算符重载）
- **`IAtom extends IXYZ`** — 坐标有了"身份"：`type()` 种类编号，可选 `id()`、速度、符号。从纯几何量变成了一个物理原子
- **`IBox extends IXYZ`** — 坐标变成了"空间"：x/y/z 对应正交盒的三边长，额外提供基向量 `a/b/c()`、倾斜分量 `xy/xz/yz()`、体积 `volume()`。

```groovy
IAtomData data = ...                              // 从文件读取或晶格构造获得
IBox box = data.box()                             // 获取模拟盒
IAtom a0 = data.atom(0)                           // 获取第 0 个原子（IXYZ + type + ...）

// IAtom 可直接当坐标做向量运算
IAtom a1 = data.atom(1)
double d = a0.distance(a1)                        // 原子间距

// IBox 坐标变换（就地修改）
XYZ r = new XYZ(a0)                               // 复制取出坐标
box.wrapPBC(r)                                    // 绕回盒内
box.toDirect(r)                                   // 转为 fractional
```

> `toDirect()` 变换后对各分量做浮点误差贴靠（DBL_EPSILON 容差内贴靠到最近整数，包括所有整数值），确保 `wrapPBC` 在边界处的 `floor` 判据不被浮点误差干扰。复杂建模中可直接依赖此行为，无需自行处理边界浮点容差

## 只读与可写镜像设计

jse 的原子相关接口普通采用"只读接口 / 可写接口"成对设计：

```
IXYZ  ←  ISettableXYZ        （坐标）
IAtom ←  ISettableAtom        （原子，继承坐标链）
IAtomData ← ISettableAtomData （原子数据容器）
IAtomDataOperation ← ISettableAtomDataOperation （运算器）
```

只读侧提供访问方法，可写侧增加 setter、`2this` 就地修改、链式返回。从 `IAtomData` 取出的 atom/op 是只读的 `IAtom`/`IAtomDataOperation` ；从 `ISettableAtomData` 取出的 atom/op 则是可写入的 `ISettableAtom`/`ISettableAtomDataOperation` 引用，修改即生效。

```groovy
ISettableAtomData data = ... 
ISettableAtom a = data.atom(0)
a.setX(5.0d)               // 就地回写到 data，不需要 data.setAtom(0, a)
```

## 构造与初始化结构

### 标准晶格：Structures

`Structures` 生成 BCC/FCC/SC/HCP 晶格，返回 `IAtomData`：

```groovy
IAtomData fcc = Structures.fcc(4.05d, 3)          // FCC 等重复 3×3×3
IAtomData bcc = Structures.bcc(3.16d, 2, 3, 2)    // BCC x/y/z 独立重复
IAtomData hcp = Structures.hcp(2.5d, 3)           // HCP 自动 c/a 高度
```

> HCP 内部将六角晶胞正交化以便直接使用笛卡尔坐标，默认高度以理想 c/a 比自动计算。如需指定高度用 `Structures.hcp(cellSize, cellHeight, repeat)`。
> 
> 扩胞优先使用 `op().repeat()`（见下方基础结构变换），不建议用 `Structures.from()`。

### 手动构造：AtomData.builder()

通用的自定义情况则使用 builder。优先用 `add()`（非 `addAtom()`），`<<` 仅用于搬运已有原子。建议先设元数据再添加原子：

```groovy
ISettableAtomData data = SettableAtomData.builder()
    .setSymbols("Cu", "Ni")
    .setBox(10.0d, 10.0d, 10.0d)
    .add(0.0d, 0.0d, 0.0d, 1)           // (x, y, z, type)
    .add(1.0d, 1.0d, 1.0d, 2)
    ...
    .build()

// << 用于从已有容器搬运原子（注意 Groovy 优先级，<< 不宜和 .build() 直接链式）
def builder = SettableAtomData.builder().setBox(10.0d, 10.0d, 10.0d)
builder << data.atom(2) << data.atom(5)
ISettableAtomData subset = builder.build()
```

不可变容器用 `AtomData.builder()`，流程相同。

## 修改模拟盒

`ISettableAtomData` 的 `setBox` 族支持修改已有数据的模拟盒。所有方法接受可选的 `boolean aKeepAtomPosition`（默认 `false`）：`false` 时原子坐标随盒等比拉伸（fractional 坐标不变），`true` 时保持原子不动。

正交盒用 `setBox(x, y, z)`（会丢弃已有倾斜数据）；仅改边长保留倾斜用 `setBoxXYZ(x, y, z)`；三斜盒用基向量 `setBox(a, b, c)` 或 lammps 风格 `setBox(x, y, z, xy, xz, yz)`。`setBoxScale(scale)` 等比例缩放，`setBoxNormal()` / `setBoxPrism()` 在正交与三斜之间转换。

```groovy
ISettableAtomData data = ...

data.setBox(20.0d, 20.0d, 20.0d)           // 正交，原子随盒拉伸
data.setBox(true, 20.0d, 20.0d, 20.0d)     // 正交，原子不动
data.setBoxXYZ(15.0d, 15.0d, 20.0d)        // 仅改边长，保留倾斜
data.setBoxScale(2.0d)                      // 等比例缩放
```

> 完整重载见 `api/jse/atom/isettableatomdata.md`。

## 修改种类与符号

`ISettableAtomData` 支持修改种类符号、质量和速度标记。

`setSymbols("Cu", "Ni")` 按种类编号设置符号（索引 0 对应 type 1），不改变已有原子的 type 值——只改标签不改数据。`setSymbolOrder("Ni", "Cu")` 则会调整符号→类型的映射，重映射原子的 type 编号。`setNtypes(n)` 扩展或收缩种类数（收缩时超出种类的原子截断为 n）。

```groovy
ISettableAtomData data = ...

data.setSymbols("Cu", "Ni")        // type1=Cu, type2=Ni
data.setSymbolOrder("Ni", "Cu")    // 交换映射，type1 变为 Ni
data.setNtypes(2)                  // 收缩为 2 种
data.setNoSymbol()                 // 清除符号信息
```

质量通常由元素符号按 `CS.MASS` 自动推导，无需手动设置；需要手动指定时用 `setMasses`（如 `Lmpdat`）。速度方面（如 `setHasVelocity()`）仅 `DataXYZ`、`Lmpdat` 等格式类型支持。

> 完整签名及 `setSymbols`/`setSymbolOrder` 精确语义差异见 `api/jse/atom/isettableatomdata.md`。

## 基础结构变换

`op()` 是结构级操作的统一入口。`IAtomData.op()` 返回 `IAtomDataOperation`，所有操作默认**返回新数据**，不修改原数据。`ISettableAtomData.op()` 返回 `ISettableAtomDataOperation`，在此基础上额外提供 `2this` 后缀的就地修改版本。

### PBC 操作

将超出盒边界的原子绕回盒内：

```groovy
IAtomData wrapped = data.op().wrap()             // 返回新数据
// ISettableAtomData 可用：
data.op().wrap2this()                            // 直接修改 data
```

### 扩胞与切块

超胞扩胞，生成周期性重复结构：

```groovy
IAtomData expanded = data.op().repeat(3, 3, 3)   // 或 repeat(n) 三个方向等重复
```

均分切块，将体系按指定份数均匀拆分：

```groovy
List<? extends ISettableAtomData> blocks = data.op().slice(2, 2, 2)
```

### 种类过滤

按种类过滤，保留指定 type 的原子：

```groovy
IAtomData type2 = data.op().filterType(2)
```

### 种类变换

按闭包逐原子映射种类，或按权重随机分配：

```groovy
data.op().mapType { atom -> atom.type() == 2 ? 1 : atom.type() }
data.op().mapTypeRandom(8, 2)                    // 按 8:2 权重随机分配
```

> `POSCAR` 中 `2this` 版本修改 type 为未定义行为 — `POSCAR` 类型由于设置种类的实现方式原因，在 `mapType2this`/`mapTypeRandom2this` 中会产生未定义行为，详见 `atom2.md`。


### 坐标扰动

对原子坐标施加高斯随机位移：

```groovy
IAtomData noisy = data.op().perturbXYZ(0.01d)    // sigma = 0.01 Å
```

### 团簇分析

按截断距离识别连通团簇，返回各团簇的原子索引列表：

```groovy
List<IntVector> clusters = data.op().clusterAnalyze(3.5d)
```

按团簇将 PBC 拆分的原子组展开到连续空间：

```groovy
IAtomData unwrapped = data.op().unwrapByCluster(2.0d)  // 2.0: 团簇判据截断半径
```
