# jse — 启动入口与脚本执行

jse 的主要启动方式、脚本语言选择、交互入口和少量环境维护入口。

> **类引用**：`SP`=`jse.code.SP`，`OS`=`jse.code.OS`

## 核心取向

jse 是以 Groovy 脚本为主线的执行入口，同时支持 Python 脚本。jse 通过内嵌 Groovy 解释器（GroovyShell）执行 `.groovy` 脚本，通过 jep 内嵌 CPython 执行 `.py` 脚本。

## 脚本执行入口

日常优先直接执行脚本文件，语言由后缀自动判定：

```bash
jse script.groovy               # .groovy → Groovy
jse script.py                   # .py / .jsepy → Python
jse script                      # 无后缀 → 优先 Groovy
```

脚本参数直接附加在路径之后：

```bash
jse script.groovy arg1 arg2
```

只有当自动判断不符合预期时才显式指定语言：

```bash
jse --groovy script             # 强制 Groovy（不指定路径时启动 groovysh）
jse --python script             # 强制 Python（不指定路径时启动 Python Shell）
```

> Agent 下注意避免进入交互式 shell

`-f` / `--file` 用于显式表达脚本文件，与默认执行行为一致：

```bash
jse -f script.groovy arg1 arg2  # 等价于 jse script.groovy arg1 arg2
```

## 文本片段与交互入口

文本片段适合快速验证或一次性调用：

```bash
jse -t 'println(CS.VERSION)'           # Groovy 文本
jse --pythontext 'print("hello")'      # Python 文本
```

> Groovy 文本注意避免遗漏导入或者使用完整包名。
> 
> 第一次执行 Python 文本会触发 JEP JNI 初始化，具体见 `python.md`。

Shell 中字符串二次解析可能导致引号冲突，可临时使用 Groovy 斜杠字符串绕开：

```bash
jse -t 'println(/hello world/)'
```

## 环境维护入口

```bash
jse -v                      # 版本信息
jse -?                      # 帮助
jse --jnibuild              # 构建所有 JNI 库（JEP/MPI/LMP/NNAP）
jse --jniclean              # 清理 JNI 缓存
jse --jupyter               # 安装当前 jse 到 Jupyter kernel
jse --idea                  # 初始化当前目录为 IntelliJ IDEA 项目
jse -lmp -in melt.in        # 启动内嵌 LAMMPS
```

`--jnibuild` / `--jniclean` 涉及交互式确认，应由用户手动执行，不在脚本中自动调用。LAMMPS、Jupyter 的具体用法见各自专题文档。

## 自定义 JVM 启动方式

默认 JVM 参数适合大多数场景。需要调整堆内存、GC 等参数时，**不要直接修改原始启动脚本**，应参考以下策略自建启动包装：

1. 读取原有启动脚本了解 JVM 参数设置方式
2. 通过 `OS.JAR_PATH` 定位核心 jar
3. 结合两者编写自定义启动脚本

```bash
# 查看启动脚本
cat $(which jse)

# 获取核心 jar 路径（完整包名避免导入）
jse -t 'println(jse.code.OS.JAR_PATH)'
```

Windows PowerShell 下同理：

```powershell
Get-Content (Get-Command jse).Source
```
