# NEP

> `jsex.nep.NEP`

**核心职能**：`implements IPairPotential`。包装 GPUMD NEP_CPU 的 C++ 实现，通过 JIT（CPU 用 SimpleJIT，CUDA 用 CudaJIT）运行时编译生成 native 库。构造时解析 `nep.txt` 势文件（参数、ANN 权重、描述符），自动编译并加载。支持 `calEnergy`（纯能量）和 `calEnergyForceVirial`（能量+力+维里）两种计算模式。

```java
// === 构造 ===
NEP(String aPotentialFileName)                  // 从 nep.txt 初始化，默认 CPU 架构 + double 精度

// === IPairPotential 基础查询 ===
int ntypes()                                    // 元素种类数
boolean hasSymbol()                             // 总是返回 true
String symbol(int aType)                        // 第 aType 种元素的符号（1-indexed）
double rcutMax()                                // 截断半径 = max(rc_radial, rc_angular)

// === 能量与力计算（IPairPotential 实现） ===
void calEnergy(int aAtomNumber, INeighborListGetter aNeighborListGetter, IEnergyAccumulator rEnergyAccumulator)
void calEnergyForceVirial(int aAtomNumber, INeighborListGetter aNeighborListGetter, @Nullable IEnergyAccumulator rEnergyAccumulator, @Nullable IForceAccumulator rForceAccumulator, @Nullable IVirialAccumulator rVirialAccumulator)

// === 生命周期 ===
boolean isClosed()                              // 是否已关闭
void close()                                    // 释放 JIT 引擎、指针、CUDA 资源

// === 全局配置 ===
static class Conf {
    static int CUDA_BLOCKSIZE                   // CUDA block_size, 默认 256 (JSE_NEP_CUDA_BLOCKSIZE)
    static boolean USE_TABLE_FOR_RADIAL_FUNCTIONS // 查表法计算径向函数, 默认 false (JSE_NEP_USE_TABLE_FOR_RADIAL_FUNCTIONS)
    static Map<String, String> CMAKE_SETTING     // 自定义 cmake -D 参数 (JSE_CMAKE_SETTING_NEP)
    static @Nullable String CMAKE_CXX_COMPILER   // C++ 编译器 (JSE_CMAKE_CXX_COMPILER_NEP)
    static @Nullable String CMAKE_CXX_FLAGS      // C++ 编译参数 (JSE_CMAKE_CXX_FLAGS_NEP)
    static @Nullable String CMAKE_CUDA_COMPILER  // CUDA 编译器 (JSE_CMAKE_CUDA_COMPILER_NEP)
    static @Nullable String CMAKE_CUDA_FLAGS     // CUDA 编译参数 (JSE_CMAKE_CUDA_FLAGS_NEP)
    static int OPTIM_LEVEL                       // 优化等级, 默认 IJITEngine.OPTIM_BASE (JSE_NEP_OPTIM_LEVEL)
    static String PRECISION                      // CPU 精度 "double"/"single", 默认 "double" (JSE_NEP_PRECISION)
}
```
