---
name: jse-skill
description: jse（Java Simulation Environment）开发助手 — 科学模拟脚本、数据分析处理、跨语言（Groovy/Python）编程
trigger: jse|\.groovy|\.jsepy|\.jnn|lammps|lmp|ase|vasp|nep|nnap|eam|xyz|poscar|xdatcar
---

# jse 开发

面向使用 jse 编写 Groovy / Python 科学模拟脚本的助手。

## 信息检索

查询接口和编写代码时严格按以下顺序：

```
doc_agent/  →  api/  →  _src/
```

1. **doc_agent/** — 按任务关键词匹配领域文档，建立领域认知和使用模式
2. **api/** — 按包路径定位类文件，确认方法签名和返回值类型（目录结构与 Java 包层级一一对应，文件名全小写、下划线分隔内部类）
3. **_src/** — 仅在前两层信息不足时才读 Java 源码，**禁止直接跳读源码**

## 文档索引与格式

### doc_agent/ 已有文档

编写新文档前必须通读其**前置文档**——编号相连的上下篇、跨文档引用的目标、同领域关联文档。

- `main.md` — jse 执行 Groovy / Python 脚本的方式
- `python.md` — Python 脚本使用方式，jse/Groovy ↔ Python 互操作
- `util.md` — 核心工具类：CS 常量、Conf 配置、UT 方法、OS 平台判定
- `io.md` — 通用文件读写
- `system.md` — 系统命令执行基础
- `system2.md` — 进阶系统命令（Slurm 调度、SSH 远程执行）
  - 前置：`system.md`
- `math.md` — 基本数学库：IVector 向量、IMatrix 矩阵、UT.Math、MathEX
- `math2.md` — 进阶数学：特化向量/矩阵、IDataShell 输入、Table 表格、Func1/2、Complex
  - 前置：`math.md`
- `math3.md` — 高级数学：NumPy 互操作与线性代数：jse ↔ NumPy 数据转换、调用策略、边界处理
  - 前置：`math.md`、`math2.md`、`python.md`
- `atom.md` — 原子结构基础
- `atom2.md` — 具体原子结构实现细节，不同格式的读写与互转
  - 前置：`atom.md`
- `MAIN_groovy.md` — Groovy 脚本编码硬约束

### api/ 签名参考格式

- **标题**："## `jse.xxx`" + "> blockquote" + "概述职能"；类标题统一 "### OuterClass.InnerClass — 职能"
- **签名块**：平铺方法签名以及必要说明注释
- **文件定位**：目录结构镜像 Java 包层级，文件名全小写、下划线分隔内部类（`jse.code.SP.Python` → `api/jse/code/sp_python.md`）；每个包提供 `_intro.md` 展示架构总览和继承关系
- **关键提示**：`// :note:` 前缀为用户额外添加的重点提示

## 编码硬约束

编写 Groovy 脚本时严格遵守 `doc_agent/MAIN_groovy.md`：

- 函数调用必须有括号：`println('Hello')` 非 `println 'Hello'`
- 函数参数加显式类型：`void foo(double x)` 非 `def foo(x)`
- 浮点数字面量加 `d` 后缀：`3.5d` 非 `3.5`
- 一般循环用 range：`for (i in 0..<n) { }`；计算密集用 `@CompileStatic` + C风格
- 函数定义放脚本末尾，优先使用 jse 内置库

## 注意事项

- 严格遵守信息检索的三层优先级 `doc_agent/ → api/ → _src/`
- 不确定的 API 先查 `api/`，禁止凭惯用命名猜测，**禁止直接跳读源码**
- 涉及 CPointer、MPI 等 native 数据输入时，优先识别 `Vector`/`IntVector` 与 `DoubleList`/`IntList` 等 `IDataShell` 容器；脚本层只使用其普通向量/List 接口，不展开 `IDataShell` 底层方法
- 涉及 JNI（JEP/MPI/LMP/NNAP）的功能需用户先执行 `jse --jnibuild`
