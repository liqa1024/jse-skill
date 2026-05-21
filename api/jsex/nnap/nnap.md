# NNAP

> `jsex.nnap.NNAP`

> 此类标记为 `@ApiStatus.Experimental`

**核心职能**：`implements IPairPotential`。多元素神经网络原子势，通过 JIT 编译 C++ 代码实现。构造时加载 JSON/YAML 模型文件或 Map 配置，解析 Basis + NeuralNetwork 参数、描述符权重及归一化系数，自动 JIT 编译 native 库。支持 `calEnergy`/`calEnergyForceVirial` 标准接口，以及 `calFp` 批量描述符计算。内置参数/梯度管理体系（`requireGrad`/`zeroGrad`/`backwardParameter`）供 Trainer 使用。

```java
// === 构造 ===
NNAP(Map<?, ?> aModelInfo)                      // 从 Map 配置初始化，单线程
NNAP(String aModelPath)                         // 从 JSON/YAML 文件初始化，单线程
NNAP(Map<?, ?> aModelInfo, int aNumThreads)     // 指定线程数（≥1）
NNAP(String aModelPath, int aNumThreads)        // 文件 + 线程数

// === IPairPotential 基础查询 ===
int ntypes()                                    // 元素种类数
boolean hasSymbol()                             // 总是返回 true
String symbol(int aType)                        // 第 aType 种元素的符号（1-indexed）
double rcutMax()                                // 最大截断半径（所有 basis 中的最大值）
int nthreads()                                  // 线程数
String units()                                  // 势函数单位（如 "metal"），可能为 null
String precision()                              // 精度 "single" 或 "double"
double rcut(int aType)                          // 第 aType 种元素的截断半径

// === 能量与力计算（IPairPotential 实现） ===
void calEnergy(int aAtomNumber, INeighborListGetter aNeighborListGetter, IEnergyAccumulator rEnergyAccumulator)
void calEnergyForceVirial(int aAtomNumber, INeighborListGetter aNeighborListGetter, @Nullable IEnergyAccumulator rEnergyAccumulator, @Nullable IForceAccumulator rForceAccumulator, @Nullable IVirialAccumulator rVirialAccumulator)

// === 描述符计算 ===
List<Vector> calFp(IAtomData aAtomData)         // 计算所有原子的描述符向量，自动处理元素映射

// === 参数与梯度管理 ===
IVector parameters()                            // 可训练参数向量（只读视图）
IVector gradParameters()                        // 梯度向量（需先调用 requireGrad()）
void initParameters()                           // 随机初始化 Basis + NN 参数
void updateParameters()                         // 将参数同步到 C 指针
void backwardParameter()                        // 将梯度从 C 指针反向同步到 gradParameters()
void requireGrad()                              // 分配梯度缓存（重复调用为 no-op）
void zeroGrad()                                 // 清零所有梯度

// === 归一化系数 ===
double normMuEng(int aType)                     // 第 aType 种元素的能量均值归一化系数
void setNormMuEng(int aType, double aValue)
double normSigmaEng(int aType)                  // 第 aType 种元素的能量标准差归一化系数
void setNormSigmaEng(int aType, double aValue)
IDoubleOrFloatCPointer normMu(int aType)        // 基组归一化均值向量指针
IDoubleOrFloatCPointer normSigma(int aType)     // 基组归一化标准差向量指针

// === 底层 JIT 调用（多由 Trainer 内部使用） ===
void calFp(int aThreadID, IDoubleOrFloatCPointer aNlDx, IDoubleOrFloatCPointer aNlDy, IDoubleOrFloatCPointer aNlDz, IntCPointer aNlType, int aNumNei, int aCType, IDoubleOrFloatCPointer rFp)
double calEnergy(int aThreadID, IDoubleOrFloatCPointer aNlDx, IDoubleOrFloatCPointer aNlDy, IDoubleOrFloatCPointer aNlDz, IntCPointer aNlType, int aNumNei, int aCType)
double calEnergyForce(int aThreadID, IDoubleOrFloatCPointer aNlDx, IDoubleOrFloatCPointer aNlDy, IDoubleOrFloatCPointer aNlDz, IntCPointer aNlType, int aNumNei, int aCType, IDoubleOrFloatCPointer rGradNlDx, IDoubleOrFloatCPointer rGradNlDy, IDoubleOrFloatCPointer rGradNlDz)
double forwardEnergy(int aThreadID, IDoubleOrFloatCPointer aNlDx, IDoubleOrFloatCPointer aNlDy, IDoubleOrFloatCPointer aNlDz, IntCPointer aNlType, int aNumNei, int aCType, IGrowableDoubleOrFloatCPointer rCaches)
void backwardEnergy(int aThreadID, double aGradEng, IDoubleOrFloatCPointer aNlDx, IDoubleOrFloatCPointer aNlDy, IDoubleOrFloatCPointer aNlDz, IntCPointer aNlType, int aNumNei, int aCType, IDoubleOrFloatCPointer aCaches)
double forwardEnergyForce(int aThreadID, IDoubleOrFloatCPointer aNlDx, IDoubleOrFloatCPointer aNlDy, IDoubleOrFloatCPointer aNlDz, IntCPointer aNlType, int aNumNei, int aCType, IGrowableDoubleOrFloatCPointer rCaches, IDoubleOrFloatCPointer rAGradNlDx, IDoubleOrFloatCPointer rAGradNlDy, IDoubleOrFloatCPointer rAGradNlDz)
void backwardEnergyForce(int aThreadID, double aBGradEng, IDoubleOrFloatCPointer aNlDx, IDoubleOrFloatCPointer aNlDy, IDoubleOrFloatCPointer aNlDz, IntCPointer aNlType, int aNumNei, int aCType, IDoubleOrFloatCPointer aCaches, IDoubleOrFloatCPointer aBGradAGradNlDx, IDoubleOrFloatCPointer aBGradAGradNlDy, IDoubleOrFloatCPointer aBGradAGradNlDz)

// === 生命周期 ===
boolean isClosed()                              // 是否已关闭
void close()                                    // 释放 JIT 引擎、指针、缓存

// === 全局配置 ===
static class Conf {
    static Map<String, String> CMAKE_SETTING     // 自定义 cmake -D 参数 (JSE_CMAKE_SETTING_NNAP)
    static @Nullable String CMAKE_CXX_COMPILER   // C++ 编译器 (JSE_CMAKE_CXX_COMPILER_NNAP)
    static @Nullable String CMAKE_CXX_FLAGS      // C++ 编译参数 (JSE_CMAKE_CXX_FLAGS_NNAP)
    static int OPTIM_LEVEL                       // 优化等级, 默认 IJITEngine.OPTIM_BASE (JSE_NNAP_OPTIM_LEVEL)
    static String PRECISION                      // CPU 精度 "double"/"single", 默认 "double" (JSE_NNAP_PRECISION)
}
```
