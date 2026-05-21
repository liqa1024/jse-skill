# `jse.jit`

> JIT 编译引擎——将 C++ 源码字符串运行时编译为动态库并加载，通过 `IJITMethod.invoke(IPointer,IPointer)→int` 调用编译后的函数。`SimpleJIT.Engine` 提供 fluent 构建器模式，支持四级优化（NONE/COMPAT/BASE/MAX）、方法缓存、自动资源清理。底层通过 cmake+ninja 编译。
