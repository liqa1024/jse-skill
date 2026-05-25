# jse — 具体势函数实例

LJ、Soft、EAM 为 jse 内置的纯 Java `IPairPotential` 实现，覆盖从简单两体势到嵌入原子势的常见需求。

> **类引用**：`LJ`=`jse.atom.pot.LJ`，`Soft`=`jse.atom.pot.Soft`，`EAM`=`jse.atom.pot.EAM`，`IPairPotential`=`jse.atom.IPairPotential`，`APC`=`jse.atom.APC`

## LJ

Lennard-Jones 12-6 势：

$$
E = 4\varepsilon \left[ \left( \frac{\sigma}{r} \right)^{12} - \left( \frac{\sigma}{r} \right)^6 \right]
$$

单参数版适用于单元素体系；种类依赖版通过下三角矩阵 `eps[i][j]`/`sigma[i][j]`/`rCut[i][j]` 为每对种类指定参数。`setShift()` 在截断处做能量平移使势能平滑归零：

```groovy
LJ lj1 = new LJ(0.5d, 3.0d, 6.0d)                  // 单参数
lj1.setShift()                                       // 截断处能量平移

double[][] eps   = [[0.5d, 0.3d], [0.3d, 0.4d]]      // 下三角：1-1, 2-1, 2-2
double[][] sigma = [[3.0d, 2.8d], [2.8d, 3.2d]]
double[][] rCut  = [[6.0d, 6.0d], [6.0d, 6.0d]]
LJ lj2 = new LJ(eps, sigma, rCut)                    // 种类依赖
lj2.setNthreads(4)
```

`manybody=false`，`neighborListHalf=true` 利用牛顿第三定律只遍历半边近邻列表。

## Soft

余弦软势，仅排斥分支，用于推开初始结构中过近的原子：

$$
E = A \left[ 1 + \cos\left( \frac{\pi r}{r_c} \right) \right] \quad (r < r_c)
$$

构造模式与 LJ 相同——单参数或种类依赖矩阵：

```groovy
Soft soft = new Soft(1.0d, 3.0d)                     // 单参数

double[][] A    = [[1.0d, 0.5d], [0.5d, 2.0d]]
double[][] rCut = [[3.0d, 3.0d], [3.0d, 3.0d]]
Soft soft2 = new Soft(A, rCut)                        // 种类依赖
```

## EAM

嵌入原子势（[Embedded Atom Method](https://en.wikipedia.org/wiki/Embedded_atom_model)），以 `alloy` 格式为例：

$$
E = \sum_i F_k(\rho_i) + \frac{1}{2} \sum_{i \neq j} \varphi_{k_i k_j}(r_{ij}), \quad \rho_i = \sum_{j \neq i} \rho_{k_j}(r_{ij})
$$

其中 $k$ 为元素种类，$F_k$ 为种类依赖的嵌入能，$\varphi_{k_i k_j}$ 和 $\rho_{k_j}$ 为种类依赖的对势和密度函数。`eam`/`alloy`/`fs`/`adp` 公式和文件存储格式存在细微区别，详见 LAMMPS [pair_eam](https://docs.lammps.org/pair_eam.html) 以及 [pair_adp](https://docs.lammps.org/pair_adp.html) 文档。

文件读取时格式自动检测，也可显式指定：

```groovy
EAM eam = new EAM("Fe.eam.fs")                       // 自动检测
EAM eam2 = new EAM("Ni.eam.alloy", "alloy")          // 显式指定
eam.setNthreads(4)
```

内部对表格化的 $F(\rho)$、$\rho(r)$、$\varphi(r)$ 使用样条插值计算（`EAM.Conf.USE_SPLINE` 控制，默认 `true`）。

## 机器学习势

NEP 和 NNAP 均实现 `IPairPotential`，基于 C++ 后端通过 JIT 编译为 native 库调用：

- **NEP** — Neuroevolution Potential，基于 GPUMD NEP_CPU 实现，支持 `nep3`/`nep4`/`nep5` 势文件
- **NNAP** — Neural Network Atomic Potential，多元素体系，含完整训练框架

均支持 CPU double/single 精度。详见 `nep.md` / `nnap.md`。

## LAMMPS / ASE 计算器

`LmpPotential` / `SystemLmpPotential` 将 LAMMPS pair-style 包装为 `IPotential`；`AseCalculator` 将 ASE calculator 包装为 `IPotential`。`IPotential.ase()` 提供反向转换（jse → ASE calculator）。详见 `lmp.md` / `ase.md`。
