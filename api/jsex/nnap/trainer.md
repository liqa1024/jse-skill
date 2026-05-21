# Trainer

> `jsex.nnap.Trainer`

**核心职能**：`implements IHasSymbol, ISavable, AutoCloseable`。纯 jse + JIT 实现的 NNAP 端到端训练器。支持能量/力/应力联合训练，内置 LBFGS 和 Adam 优化器，自动归一化基组与能量，支持早停与 batch 训练。通过 `addTrainData`/`addTestData` 添加数据后调用 `train` 开始训练。

```java
// === 损失函数（静态常量） ===
static ILossFunc LOSS_SQUARE                   // MSE: (pred-real)²
static ILossFunc LOSS_ABSOLUTE                 // MAE: |pred-real|
static ILossFunc LOSS_SMOOTHL1                 // Smooth L1 (Huber)

@FunctionalInterface interface ILossFunc {
    double call(double aPred, double aReal, DoubleWrapper rGrad)
}

// === 构造 ===
Trainer(Map<String, ?> aArgs)                   // 新训练，aArgs 含 symbols/basis/nn/optimizer 等
Trainer(Map<String, ?> aArgs, @Nullable Map<String, ?> aModelInfo) // 继续训练（retrain）

// === 数据添加 ===
void addTrainData(IAtomData aAtomData, double aEnergy, @Nullable IMatrix aForces, @Nullable IVector aStress)
void addTrainData(IAtomData aAtomData, double aEnergy, IMatrix aForces)
void addTrainData(IAtomData aAtomData, double aEnergy)
void addTestData(IAtomData aAtomData, double aEnergy, @Nullable IMatrix aForces, @Nullable IVector aStress)
void addTestData(IAtomData aAtomData, double aEnergy, IMatrix aForces)
void addTestData(IAtomData aAtomData, double aEnergy)

// === 训练配置（链式调用） ===
Trainer setEnergyWeight(double aWeight)         // 能量 loss 权重, 默认 1.0
Trainer setForceWeight(double aWeight)          // 力 loss 权重, 默认 0.1
Trainer setStressWeight(double aWeight)         // 应力 loss 权重, 默认 0.1
Trainer setLossFunc(ILossFunc aLossFunc)        // 统一设置能量/力/应力 loss
Trainer setLossFuncEnergy(ILossFunc aLossFunc)  // 单独设置能量 loss
Trainer setLossFuncForce(ILossFunc aLossFunc)   // 单独设置力 loss
Trainer setLossFuncStress(ILossFunc aLossFunc)  // 单独设置应力 loss
Trainer setOptimizer(Map<String, ?> aOptArgs)   // 设置优化器 type: "lbfgs"/"adam", lr, batch_size 等
Trainer setLearningRate(double aLearningRate)   // 设置学习率
Trainer setBatchSize(int aBatchSize)            // 设置 batch_size（-1 为全量）
Trainer setBasisMax(double aValue)              // 基组归一化最大值限制, 默认 5.0
Trainer setShareNorm(boolean aFlag)             // 是否共享归一化系数
Trainer setAutoBreak(boolean aFlag)             // 是否自动早停, 默认 true
Trainer reset()                                 // 重置优化器状态

// === 训练 ===
void train(int aNEpochs)                        // 训练 aNEpochs 个 epoch（默认早停+打印）
void train(int aNEpochs, boolean aEarlyStop)    // 可选早停
void train(int aNEpochs, boolean aEarlyStop, boolean aPrintLog) // 全参数

// === 查询 ===
NNAP model()                                    // 获取底层 NNAP 模型
int ntypes()                                    // 元素种类数
String symbol(int aType)                        // 元素符号
boolean hasSymbol()
String units()                                  // 单位
String precision()                              // 精度
IVector trainLoss()                             // 训练集历史 loss
IVector testLoss()                              // 测试集历史 loss

// === 速度统计 ===
double statSpeed(double aMaxTimeSecond)         // 统计力计算速度 (atom-steps/ms)
double statSpeed(boolean aTest, double aMaxTimeSecond)

// === 保存 ===
void save(Map rSaveTo)                          // 序列化到 Map（含 basis/nn/norm/ref_eng）
void save(String aPath)                         // 保存为 JSON
void save(String aPath, boolean aPretty)        // 可选 pretty-print

// === 生命周期 ===
void close()                                    // 释放线程池、缓存、数据集
```
