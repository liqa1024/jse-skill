# jse — Python 互操作

jse 通过 Jep 嵌入 CPython，Groovy 与 Python 共享同一 JVM 进程，可直接相互调用。本文关注"使用路径选择"：命令行执行、Groovy 调 Python、Python 调 jse 核心、少数 Python 调 Groovy 场景。

> **类引用**：`SP`=`jse.code.SP`，`SP.Python`=`jse.code.SP.Python`，`SP.Groovy`=`jse.code.SP.Groovy`，`PyObject`=`jep.python.PyObject`，`Python`=`jse.system.Python`，`JSESystemExecutor`=`jse.system.JSESystemExecutor`

## 环境与验证

jse 的 Python 支持依赖 JEP JNI 编译。首次使用或全新环境时，需用户确认已运行过：

```bash
jse --jnibuild
```

该命令会检测 Python 环境、编译 JNI 库。之后正常启动 jse 时会自动初始化 Jep 解释器，无需额外操作。

> ⚠️ **TODO(jse)**：目前无 API 可在不触发初始化的前提下预检 JNI 是否已构建。`SP.Python.InitHelper.initialized()` 仅判断静态初始化是否已执行，无法检测磁盘上的库是否存在。未构建时直接调用 Python 相关功能会触发交互式自动构建导致卡死。

## 执行 Python 脚本

三种入口形态（详见 `main.md`）：

```bash
jse script.py                  # .py / .jsepy 后缀 → Python
jse --python script            # 强制按 Python 执行
jse --pythontext 'print(1)'    # 直接执行 Python 文本
```

Python 脚本的 `sys.argv` 由 jse 自动设置，参数传递与 Groovy 脚本一致。`.jsepy` 后缀与 `.py` 等效，均为 Python 脚本。

## Groovy 调 Python

推荐流程为两步：先用 `SP.Python.exec` 导入模块或定义对象，再用 `SP.Python.get` 取回 Python 对象，之后按 Groovy 原生 OOP 风格调用。

```groovy
// 在 Python 解释器中导入模块
SP.Python.exec("import numpy as np")
SP.Python.exec("def add(a, b): return a + b")

// 取回 Python 对象（返回 PyObject）
def np = SP.Python.get("np")
def add = SP.Python.get("add")

// 按 Groovy OOP 风格调用 Python 对象
def arr = np.array([1.0d, 2.0d, 3.0d])
def s = np.sum(arr)
def r = add(1, 2)
```

> 原理: jse 修改了 `jep.python.PyObject`，使其实现 `GroovyObject`。Groovy 侧对 PyObject 的方法调用、属性读写、下标读写会自动委托到 Python 对应机制（`getattr`/`setattr`/`__getitem__`/`__setitem__`），无需显式使用 Jep 底层 API。

`SP.Python.exec` 在全局 Python 解释器中执行代码片段。`SP.Python.get` 取回已定义的变量（模块、函数、类、值），返回 `PyObject`，后续即可用 Groovy 风格操作。

**不要把常规调用全部写成 `SP.Python.exec` 拼接字符串**。嵌在 `exec` 里的 Python 代码无法利用 Groovy 的类型检查、变量作用域和 IDE 支持，并会极大降低可读性。`exec` 是补充工具，适合模块导入、一次性定义等场景；获取到 `PyObject` 后应尽量在 Groovy 侧完成操作。

### Python kwargs 传递

调用 Python 函数需要关键字参数时，将 Groovy `Map` 放在参数列表末尾，自动映射为 Python kwargs：

```groovy
// 通过 SP.Python.invoke
// SP.Python.exec("def func(a, b=2, c=3): return a + b + c")
def r1 = SP.Python.invoke("func", 1, [c: 10])       // a=1, c=10, b 用默认值 2

// 通过 PyObject 方法调用（Map 放末尾即 kwargs）
def func = SP.Python.get("func")
def r2 = func(1, [c: 10])

// 实例化 Python 类同理
// SP.Python.exec("class MyClass:\n    def __init__(self, x, y=0): self.x = x; self.y = y")
def obj = SP.Python.newInstance("MyClass", 1, [y: 100])
```

> `SP.Python.exec` 部分仅方便演示，实际对应外部 Python 包使用；如有必要 Groovy 中优先使用 `"""` 多行字符串。

此机制是 jse 对 Jep 的扩展：`SP.Python.invoke` / `SP.Python.newInstance` 变参重载和 `PyObject.invokeMethod` 均会将末尾 `Map` 参数自动转发为 Python kwargs。

### 线程安全

`PyObject` 非线程安全，只能在创建它的线程 / 解释器上下文中使用。所属 `Interpreter` 关闭后，所有衍生的 `PyObject` 即失效。多线程场景目前走 `SP.Python.*WithInterpreter` 系列方法，每个线程自动获得独立 Jep 解释器，详细用法见 `par.md`。

## Python 调 jse 核心

Python 侧调用 jse 核心类时，使用 Jep 的常规 Java 导入方式。jse 已将 Groovy 类加载器配置到 Jep，Python 可直接 import jse 包下的类：

```python
from jse.code import OS, IO, CS, Conf
from jse.math.vector import Vectors
from jse.math.matrix import Matrices

# 执行系统命令，获取输出
lines = OS.system_str("echo hello")
for line in lines:
    print(line)

# 创建向量并运算
v = Vectors.linspace(0.0, 1.0, 5)
print(v.sum())

# 文件读写
IO.write("test.txt", "hello jse")
content = IO.readAllLines("test.txt")

# 读取配置
print(CS.VERSION)
print(Conf.DEBUG)
```

> ⚠️ **Python 中不能直接使用 Groovy 运算符重载**。绝大部分 jse 类没有专门为 Python 提供 `[]` 下标和算术运算符重载，Python 中需回退到 Java 风格方法调用（如 `v.get(0)` 代替 `v[0]`，`a.plus(b)` 代替 `a + b`）。与 Python 关键字重名的方法（如 `Vectors.from`）可通过 `getattr(Vectors, 'from')(...)` 绕行。

## Python 调 Groovy

调用现有 Groovy 库或用户 Groovy 脚本类时，在 Python 侧通过 `SP.Groovy.getClass` 获取：

```python
from jse.code import SP

# 获取 Groovy 库中定义的类（区别于 jse 核心 Java 类的直接 from import）
MyClass = SP.Groovy.getClass("my.package.MyGroovyClass")
obj = MyClass()
obj.someMethod()
```

> 区分：jse 核心 Java 类（`jse.code.OS`、`jse.math.vector.Vectors` 等）可直接 `from ... import`；Groovy 脚本/库的类需经 `SP.Groovy.getClass` 获取后再使用。

## 边缘情况与通用兜底

`SP.Python.*` 和 `SP.Groovy.*` 可覆盖 Python 关键字冲突，特定 Python/Groovy 语法不支持，Jep 自动类型转换失效等边缘问题。
