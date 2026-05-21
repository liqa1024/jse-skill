# jse Core API Index

> 供上层 Groovy 脚本调用的核心 API 参考。

## 目录结构

每个包目录下：
- `_intro.md` — 包级概述与架构总览
- `<classname>.md` — 各类/接口的 API 签名

命名规则：全小写；子类以下划线分隔（如 `ut_code.md` → `UT.Code`）；驼峰类名全小写无额外下划线（如 `iatomdata.md` → `IAtomData`）。

## jse — 核心框架

| 包 | 目录 | 说明 |
|---|---|---|
| `jse` | [jse/](jse/) | 框架根包，命令行入口 Main |
| `jse.code` | [jse/code/](jse/code/) | 全局配置、I/O、系统操作、脚本引擎、工具集 |
| `jse.code.collection` | [jse/code/collection/](jse/code/collection/) | 集合工具包，原始类型动态数组、元组 |
| `jse.code.functional` | [jse/code/functional/](jse/code/functional/) | 函数式接口（基本类型 1~4 元参数） |
| `jse.code.io` | [jse/code/io/](jse/code/io/) | 底层 I/O（字符扫描、哈希、序列化） |
| `jse.code.iterator` | [jse/code/iterator/](jse/code/iterator/) | 免装箱迭代器体系 |
| `jse.code.random` | [jse/code/random/](jse/code/random/) | 随机数生成 |
| `jse.code.timer` | [jse/code/timer/](jse/code/timer/) | 计时器 |
| `jse.atom` | [jse/atom/](jse/atom/) | 分子模拟核心——原子、坐标、模拟盒、势函数 |
| `jse.atom.data` | [jse/atom/data/](jse/atom/data/) | ext-xyz / Dump 数据格式 |
| `jse.atom.pot` | [jse/atom/pot/](jse/atom/pot/) | 势函数（EAM、LJ、Soft） |
| `jse.ase` | [jse/ase/](jse/ase/) | ASE 适配器 |
| `jse.vasp` | [jse/vasp/](jse/vasp/) | VASP 输入输出 |
| `jse.lmp` | [jse/lmp/](jse/lmp/) | LAMMPS 集成 |
| `jse.math` | [jse/math/](jse/math/) | 数学基础——复数、工具、扩展 |
| `jse.math.operation` | [jse/math/operation/](jse/math/operation/) | 数组/迭代器逐元素运算 |
| `jse.math.vector` | [jse/math/vector/](jse/math/vector/) | 向量代数 |
| `jse.math.matrix` | [jse/math/matrix/](jse/math/matrix/) | 矩阵代数 |
| `jse.math.table` | [jse/math/table/](jse/math/table/) | 表格数据结构 |
| `jse.math.function` | [jse/math/function/](jse/math/function/) | 数学函数（1~3 维） |
| `jse.cache` | [jse/cache/](jse/cache/) | 对象/数组缓存池 |
| `jse.clib` | [jse/clib/](jse/clib/) | C/C++ 编译工具链 |
| `jse.cptr` | [jse/cptr/](jse/cptr/) | C 指针 JNI 封装 |
| `jse.gpu` | [jse/gpu/](jse/gpu/) | CUDA GPU 接口 |
| `jse.jit` | [jse/jit/](jse/jit/) | 运行时编译 |
| `jse.system` | [jse/system/](jse/system/) | 外部命令执行器 |
| `jse.parallel` | [jse/parallel/](jse/parallel/) | 并行框架 + MPI |
| `jse.plot` | [jse/plot/](jse/plot/) | 二维绘图 |
| `jse.optim` | [jse/optim/](jse/optim/) | 优化器 |

## jsex — 扩展模块

| 包 | 目录 | 说明 |
|---|---|---|
| `jsex.nep` | [jsex/nep/](jsex/nep/) | NEP 神经演化势 |
| `jsex.nnap` | [jsex/nnap/](jsex/nnap/) | NNAP 神经原子势 |
| `jsex.nnap.basis` | [jsex/nnap/basis/](jsex/nnap/basis/) | NNAP 基组 |
| `jsex.nnap.nn` | [jsex/nnap/nn/](jsex/nnap/nn/) | NNAP 神经网络 |
| `jsex.voronoi` | [jsex/voronoi/](jsex/voronoi/) | 3D Voronoi 分析 |

## jep — JEP 修改

| 包 | 目录 | 说明 |
|---|---|---|
| `jep.python` | [jep/python/](jep/python/) | Python 对象封装（PyObject），jse 扩展 Groovy 集成 |
