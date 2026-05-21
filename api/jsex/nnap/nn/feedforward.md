# FeedForward

> `jsex.nnap.nn.FeedForward`

**核心职能**：多层前馈神经网络，默认隐藏层 `[32, 32]`。支持可变隐藏层数和每层宽度配置。通过 `load(int inputDim, Map)` 反序列化，`save` 序列化权重/偏置。

```java
static int[] DEFAULT_HIDDEN_DIMS = [32, 32]

static FeedForward load(int aInputDim, Map aMap) // 从 Map 反序列化
void save(Map rSaveTo)                           // 序列化（type: "feed_forward"）
int parameterSize()
int fittableParameterWeightSize()                // 仅权重（不含偏置）的参数数量
int inputSize()                                  // 输入维度

// 覆写 NeuralNetwork 的全部抽象方法
```
