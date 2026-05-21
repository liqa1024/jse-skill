# jse — 基础运行环境与通用工具

CS、Conf、OS、SP、UT 是几乎所有 jse 脚本都会用到的基础工具，本文档覆盖常量、配置、环境、临时目录、外部库、随机 ID、计时和轻量并行入口。文件 I/O、系统命令、数学函数、SLURM、Python 互调等转到对应专题文档。

> **类引用**：`CS`=`jse.code.CS`，`Conf`=`jse.code.Conf`，`OS`=`jse.code.OS`，`SP`=`jse.code.SP`，`UT`=`jse.code.UT`

## 核心取向

五个工具类的分工：

- `CS` — 编译期确定的不可变常量（版本号、元素数据、物理单位）
- `Conf` — 运行时全局配置（DEBUG、线程数、路径模板等），可通过同名环境变量在启动前设置
- `OS` — 平台判定、路径常量、环境变量读取与全局系统执行器
- `SP` — 脚本语言，管理 Groovy/Python 的启动和外部库路径
- `UT` — 脚本级轻量辅助（随机 ID、计时、进度条、本地并行）

本文不是 API 清单，完整字段和重载查 `api/jse/code/`。

## 常量、配置与环境变量

根据分工选择具体工具类：

```groovy
// 查版本、元素、物理单位 → CS
CS.VERSION
CS.SYMBOLS[0]                  // "H"
double mass = CS.MASS["Fe"]    // 55.845d

// 改变 jse 行为 → Conf
Conf.DEBUG = true              // 也对应环境变量 JSE_DEBUG
Conf.STRICT_IO = false         // JSE_STRICT_IO

// 读取启动环境 → OS.env*
String val = OS.env("MY_VAR")
int n = OS.envI("N", 10)
boolean flag = OS.envZ("FLAG")                    // true/t/on/yes/1 → true
Map<String, String> map = OS.envMap("SETTINGS")   // k1:v1,k2:v2,...

// 平台判定 → OS.IS_*
OS.IS_WINDOWS
OS.IS_MAC
```

每个 `Conf.XYZ` 对应同名环境变量 `JSE_XYZ`，启动前设置后脚本中通过 `Conf.XYZ` 读取。

## 路径与临时目录

jse 路径常量均为绝对路径，目录常量统一以 `/` 结尾，可直接拼接文件名，常用路径有：

```groovy
OS.WORKING_DIR      // 工作目录
OS.JAR_DIR          // jse jar 所在目录
OS.JAR_PATH         // jse jar 文件路径
OS.USER_HOME_DIR    // 用户目录
OS.JAVA_HOME_DIR    // JDK 路径
```

路径规范化、读写、创建和删除见 `io.md`。

`Conf.WORKING_DIR_OF` 用于生成临时工作目录路径，不负责创建或清理：

```groovy
String dir = Conf.WORKING_DIR_OF(UT.Code.randID())
// → "/path/to/working/dir/.temp/a1b2c3d4e5f6g7h8/"

// ... 使用目录 ...

IO.rmdir(dir)   // 清理
```

> `Conf.WORKING_DIR_OF` 只生成路径字符串，目录由用户自行管理。模板由 `Conf.TEMP_WORKING_DIR` 控制（默认 `".temp/%n/"`）。

## 外部库路径

jse 启动时自动从 `SP` 定义的固定目录加载外部库：

```groovy
SP.GROOVY_LIB_DIR      // Groovy 脚本库（自动加入 GroovyClassLoader）
SP.PYTHON_LIB_DIR      // Python 库（自动加入 Jep include path）
```

放入以上目录的 `.groovy`、`.py` 文件在 jse 的类路径中；也可以通过 `Conf` 环境变量（`JSE_GROOVY_EXLIB_DIRS` / `JSE_PYTHON_EXLIB_DIRS`）添加自定义 Groovy / Python 库路径。

## 元素与物理单位

```groovy
// 元素符号与序号（ATOMIC_NUMBER_TO_SYMBOL 为 1-based）
CS.ATOMIC_NUMBER_TO_SYMBOL[1]   // "H"
CS.SYMBOL_TO_ATOMIC_NUMBER["He"] // 2

// 常用物理常量
CS.K_B           // Boltzmann 常数, eV/K
CS.H_BAR         // Reduced Planck 常数, eV·ps
CS.E_V           // Electron volt, g·Å²/ps²

// 能量单位换算
double energy_kcal = energy_eV * CS.EV_TO_KCAL  // eV → kcal/mol
double energy_J = energy_eV * CS.EV_TO_J        // eV → J
```

`CS.UNITS_ASE`（2014 CODATA，ASE 默认）和 `CS.UNITS`（2018 CODATA）提供完整物理常数与换算因子。`_` 前缀为基本物理常数，无前缀为单位换算因子。自定义换算参考 `EV_TO_KCAL` 的计算模式：

```groovy
double eV_to_kJ = CS.UNITS["mol"] / CS.UNITS["kJ"]
```

## 随机种子、随机 ID 与唯一 ID

三类用途：

```groovy
// randSeed — 适合模拟程序使用的随机种子
int seed = UT.Code.randSeed()              // [1, MAX_SEED]

// randID — 临时目录名、任务名、一次性输出名
String id = UT.Code.randID()               // ≤16 位十六进制随机串

// uniqueID — 基于内容决定的缓存键或结果标识
String uid = UT.Code.uniqueID(obj1, obj2)  // 深度哈希
```

MPI 并行版 `randSeed(Comm, ...)` 见 `lmp.md`。

## 计时与进度条

```groovy
// 简单耗时测量
UT.Timer.tic()
// ... 代码段 ...
UT.Timer.toc()                       // 打印 "Total time: xx sec"
double elapsed = UT.Timer.toc(true)  // 返回秒数，不打印

// 命令行进度条 — 优先使用 pbar 别名
UT.Timer.pbar("Relaxation", nsteps)
for (i in 0..<nsteps) {
    // ...
    UT.Timer.pbar()                  // 步进一步
}
```

`pbar` / `pbarw` 为 `@VisibleForTesting` 别名，Groovy 脚本优先使用。完整参数和样式控制查 `api/jse/code/ut_timer.md`。

## 轻量并行入口

`UT.Par.parfor` 适合独立循环任务：

```groovy
UT.Par.parfor(1000) { i ->
    result[i] = heavyComputation(i)
}

UT.Par.parfor(1000, 4) { i ->        // 指定线程数
    result[i] = heavyComputation(i)
}
```

线程数默认受 `Conf.PARFOR_THREAD_NUMBER` 影响。闭包中共享状态需自行保证线程安全。更多并行使用查看 `par.md`。
