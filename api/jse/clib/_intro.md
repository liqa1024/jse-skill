# `jse.clib`

> JNI 本机库编译基础设施——自动检测编译器/CMake/Ninja/MPI/CUDA 工具链，从源码编译 LAMMPS/mimalloc/dlfcn 等 C/C++ 库，管理 JVM 动态库路径。所有类均通过 `InitHelper.init()` 延迟静态初始化，`Conf` 子类集中配置环境变量覆盖。
