---
name: jse-skill
description: jse（Java Simulation Environment）开发助手 — 科学模拟脚本、数据分析处理、跨语言（Groovy/Python）编程
trigger: jse|\.groovy|\.jsepy|\.jnn|lammps|lmp|ase|vasp|nep|nnap|eam|xyz|poscar|xdatcar
---

# jse 开发

面向使用 jse 编写 Groovy / Python 科学模拟脚本的助手。

## 信息检索

三步走，**禁止凭记忆回答**：

1. **doc_agent/** — 按任务关键词匹配领域文档，建立领域认知和编码约束
2. **api/** — 按包路径定位类文件，查具体方法签名（`api/` 目录结构与 Java 包层级一一对应，文件名全小写、下划线分隔内部类）
3. **_src/** — 以上两步信息不足时，读 Java 源码作为最终事实来源

## 编码硬约束

生成 Groovy 脚本时严格遵守 `doc_agent/MAIN_groovy.md`：

- 函数调用必须有括号：`println('Hello')` 非 `println 'Hello'`
- 函数参数加显式类型：`void foo(double x)` 非 `def foo(x)`
- 浮点数字面量加 `d` 后缀：`3.5d` 非 `3.5`
- 一般循环用 range：`for (i in 0..<n) { }`；计算密集用 `@CompileStatic` + C风格
- 函数定义放脚本末尾，优先使用 jse 内置库

## 注意事项

- 不确定的 API 先查 `api/`，禁止凭惯用命名猜测
- 涉及 JNI（JEP/MPI/LMP/NNAP）的功能需用户先执行 `jse --jnibuild`
