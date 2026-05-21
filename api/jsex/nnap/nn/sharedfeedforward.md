# SharedFeedForward

> `jsex.nnap.nn.SharedFeedForward`

**核心职能**：包装一个 `FeedForward` 基网络，为非共享部分添加额外参数。`shared_hidden_dims` 数组控制每层是否共享（最后一个元素控制输出层）。提供 `full` 静态工厂创建完全共享的变体。

```java
static SharedFeedForward load(int aInputDim, NeuralNetwork[] aNN, Map aMap) // 从 Map 反序列化
static SharedFeedForward full(NeuralNetwork[] aNN, int aSharedType)         // 创建完全共享包装
void save(Map rSaveTo)                           // 序列化（type: "shared_feed_forward"）
FeedForward sharedNeuralNetwork()                // 返回被共享的基网络
int sharedType()                                 // 返回共享目标类型索引
int parameterSize()                              // 仅非共享部分的参数
int fittableParameterWeightSize()
int inputSize()

// 覆写 NeuralNetwork 的全部抽象方法
```
