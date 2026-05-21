# IJITEngine

> `jse.jit.IJITEngine`

**核心职能**：extends AutoCloseable。定义 JIT 编译的标准工作流：设置源码 → 设置优化等级 → 设置方法名列表 → `compile()` → `findMethod(name)` → 调用 → `close()` 释放动态库。

```java
// --- 优化等级常量 ---
static int OPTIM_NONE = -1      // 完全关闭优化 (调试用)
static int OPTIM_COMPAT = 0    // 兼容模式 (仅 fast-math)
static int OPTIM_BASE = 1      // 默认 (AVX2 + fast-math)
static int OPTIM_MAX = 2       // 最高 (AVX512 + fast-math, 可能更慢)

// --- 构建器 ---
IJITEngine setSrc(@Language("C++") String aSrc)             // 设置 C++ 源码（外包 `extern "C"`）
IJITEngine setOptimLevel(int aOptimLevel)                    // 设置优化等级
IJITEngine setMethodNames(String... aMethodNames)           // 设置方法名列表 (覆盖)
IJITEngine setMethodNames(Collection<? extends CharSequence>)
IJITEngine addMethodName(CharSequence aMethodName)           // 添加方法名
IJITEngine removeMethodName(CharSequence aMethodName)        // 移除方法名

// --- 查询 ---
boolean hasMethod(CharSequence aMethodName)

// --- 工作流 ---
void compile() throws Exception                              // 编译源码→动态库
IJITMethod findMethod(CharSequence aMethodName) throws JITException  // 获取方法句柄

// --- 生命周期 ---
void close() throws Exception                     // 释放动态库
boolean isClosed()
```
