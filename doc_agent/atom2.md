# jse — 原子结构文件格式

本文覆盖 jse 中主流文件格式的读写与互转：ext-xyz、LAMMPS data/dump、VASP POSCAR/XDATCAR。ASE 桥接见 `ase.md`。

> **类引用**：`DataXYZ`=`jse.atom.data.DataXYZ`，`DumpXYZ`=`jse.atom.data.DumpXYZ`，`Lmpdat`=`jse.lmp.Lmpdat`，`SubLammpstrj`=`jse.lmp.SubLammpstrj`，`Lammpstrj`=`jse.lmp.Lammpstrj`，`POSCAR`=`jse.vasp.POSCAR`，`XDATCAR`=`jse.vasp.XDATCAR`

## 格式概述与互转

所有格式类统一实现 `ISettableAtomData`，读入后与 `atom.md` 中的构造和变换无缝衔接。**禁止用 `IO.readAllLines` 手写解析**这些格式——专用类处理了坐标偏移、Direct/Cartesian 转换、种类排序等细节。

统一入口：

- `XXX.read(file)` — 从文件读取
- `XXX.of(IAtomData)` — 从已有数据转换
- `write(file)` — 写回文件

格式之间通过 `.of()` 互为转换：

```groovy
DataXYZ xyz = DataXYZ.read("input.xyz")          // read
Lmpdat lmp = Lmpdat.of(xyz)                      // of — 转换为 LAMMPS data
lmp.write("output.data")                         // write
```

各格式对 id、速度、符号、质量、键、坐标模式的保留程度不同，详见下文各节。

## 多帧轨迹

多帧格式均基于 `AbstractListWrapper`，提供统一设计。每个多帧容器对应一种单帧类型：

| 多帧容器 | 单帧类型 |
|---|---|
| `DumpXYZ` | `DataXYZ` |
| `Lammpstrj` | `SubLammpstrj` |
| `XDATCAR` | `POSCAR` |

通用操作：

- `traj[i]` — 按索引访问单帧
- `traj << frame` — 追加帧
- `traj.cutFront(n)` / `traj.cutBack(n)` — 移除前/后 N 帧
- `traj.step(n)` — 等间距采样

```groovy
Lammpstrj traj = Lammpstrj.read("dump.lammpstrj")
traj.cutFront(100)                               // 丢弃前 100 帧热化
traj.step(10)                                    // 每 10 帧取 1 帧去相关
SubLammpstrj frame0 = traj[0]                    // 索引访问单帧
traj << frame0                                   // 追加帧
traj.write("processed.lammpstrj")
```

## 各格式详情

### DataXYZ — extxyz 单帧

格式不含 id；可能包含速度、符号。可能存在自定义的参数和每原子属性。

扩展格式提供两套 key-value 系统：**参数**（`parameter`/`setParameter`，全局公用，值类型 `double/int/boolean/String`），**属性**（`property`/`setProperty`，每个原子独立，值类型 `IVector/IIntVector/IMatrix/IIntMatrix/String[]/String[][]`，按原子索引按行排列）。参数写入注释行，属性写入属性行：

```groovy
DataXYZ xyz = DataXYZ.read("input.xyz")
xyz.setParameter("energy", -123.4d)              // 设置全局参数
assert xyz.hasParameter("energy")
double e = xyz.parameter("energy")                // 读取
xyz.removeParameter("energy")                     // 删除

xyz.setProperty("forces", [0.1d, 0.2d, 0.3d])    // 设置 per-atom 属性
xyz.write("output.xyz")
```

> 同时支持普通 XYZ 和扩展 XYZ 的读取；写入时自动转为扩展格式。普通 XYZ 无模拟盒信息，读取时根据原子坐标自动生成最小正交盒。
> 
> ASE 会将 `stress` 等空格分隔字符串自行解为数组，而 jse 忠实于 extxyz 格式的字面类型，因此需要数组时需要使用 `IO.Text.str2data(xyz.parameter("stress"))` 手动解析（详见 `io.md`），而写入数组到 parameter 时可以通过 `vec.asList().join(" ")` 实现同样的效果。

### Lmpdat — LAMMPS data

固有 id；可能包含速度、质量、符号。读取时自动减下边界，脚本中盒内坐标不为负。

```groovy
Lmpdat data = Lmpdat.read("data.lmp")
assert data.hasID()
data.setMasses(55.845d, 15.999d)                // 显式设置质量 Fe, O
double xlo = data.box().xlo()                    // LmpBox 边界对访问
data.write("new_data.lmp")
```

### SubLammpstrj — LAMMPS dump 单帧

可能包含 id、速度。

可通过 `asTable()` 转为 `ITable` 直接操作原始数据列。LAMMPS dump 文件中除标准列（id、type、x、y、z...）外还可能包含用户通过 compute/fix/variable 输出的自定义列，`asTable()` 可完整读写这些列。注意 `frame.atom(i)` 获取的坐标已经过 jse 内部 shift 为非负盒内坐标，而 `asTable()` 访问的坐标列是原始值：

```groovy
SubLammpstrj frame = SubLammpstrj.read("dump.single")
LmpBox box = frame.box()                       // SubLammpstrj 同样返回 LmpBox
ITable table = frame.asTable()

// 按列名访问标准列和 LAMMPS compute/fix/variable 自定义列
IVector x = table["x"]
IVector pe = table["c_pe"]                      // compute 自定义列
IVector fx = table["f_force[1]"]                // fix 自定义列
table["pe2"] = pe * 2                           // 新增列
```

### POSCAR — VASP POSCAR

固有符号；可选 Selective dynamics。格式不含 id、速度。

底层 box 为 `VaspBox`，以 internal 坐标（`i` 前缀分量 `iax`/`iby`...）× `scale` 晶格常数存储实际坐标。坐标支持 Direct ↔ Cartesian 切换，`setCartesian()`/`setDirect()` 会自动 snap 近整数：

```groovy
POSCAR poscar = POSCAR.read("POSCAR")
poscar.setCartesian()                            // Direct → Cartesian
assert poscar.isCartesian()
double scale = poscar.box().scale()              // VaspBox 特有
```

> 无论何种模式，通过 poscar.atom(i) 获取到的坐标始终是 Cartesian 的。

> POSCAR 种类按排序分块存储，`setType` 会触发内部重排——因此直接在 POSCAR 上通过 `op().mapType2this` / `op().mapTypeRandom2this` 修改 type 将产生未定义行为。使用非 `2this` 接口或者使用 `DataXYZ.of()` 转为 extxyz 操作。
