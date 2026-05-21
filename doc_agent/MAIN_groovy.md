# jse — Groovy 编码风格指南

面向 AI Agent 生成 jse 脚本时的硬约束。

## 1. 基本规则

```groovy
// 始终使用括号
println('Hello')              // ✓
vec.add(10)                   // ✓
// println 'Hello'            // ✗

// 标准 camelCase（不用 jse 内部的 mVariable / aInput）
int atomType
double boxVolume

// 函数参数加显式类型
void updatePosition(double dt, IXYZ velocity)   // ✓
// def updatePosition(dt, velocity)             // ✗
```

优先使用 jse 内置库（`jse.code.IO` / `jse.code.OS` / `jse.math.vector` / `jse.math.matrix`），而非裸 Java 标准库。

## 2. 类型与变量

```groovy
// 基本类型一律用原始类型，浮点数加 d 后缀避免 BigDecimal
double cutoff = 3.5d
int count = 100
boolean converged = false

// 类型明确时用 def
def atoms = Lmpdat.read('system.data')
def list = [1, 2, 3]

// 空集合用显式类型
List<String> names = []

// Shell 中不用 def（否则作用域结束即丢失）
a = 10                        // ✓ Shell
// def a = 10                 // ✗ Shell
```

## 3. 循环

```groovy
// 一般逻辑 — range 风格
for (i in 0..<100) { }

// 计算密集 — C 风格 + @CompileStatic
import groovy.transform.CompileStatic

@CompileStatic
void heavyLoop(int size) {
    for (int i = 0; i < size; ++i) { }
}
```

## 4. 优先运算符重载

```groovy
// leftShift
list << item

// putAt / getAt
def v = map['key']
vec[i] = 3.14d

// plus / minus / multiply / div
def mid = (a + b) * 0.5
```

> 注意绝大部分 jse 类没有专门提供 Python 运算符重载，因此在 Python 中需要回退到类 Java 的方法调用形式。

## 5. 检查清单

在生成 Groovy 脚本后，再次检查是否满足以下要求：

- [ ] 优先使用 jse 已有实现
- [ ] 检查所有的函数调用都使用了括号调用
- [ ] 函数参数为显式类型
- [ ] 基本类型使用原始类型，并且浮点数增加 `d` 后缀避免 `BigDecimal`
- [ ] 一般循环使用 range 风格（`for (i in 0..<100) { }`）
- [ ] 调整函数定义部分在脚本最后以方便用户阅读
