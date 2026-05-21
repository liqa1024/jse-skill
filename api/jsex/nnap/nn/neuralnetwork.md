# NeuralNetwork

> `jsex.nnap.nn.NeuralNetwork`

> 此类标记为 `@ApiStatus.Experimental @ApiStatus.Internal`

**核心职能**：所有神经网络的抽象根类，`implements ISavable`。定义参数/梯度挂载协议、缓存大小查询和代码生成接口。通过 `load(Basis[], List)` 静态工厂从 JSON Map 列表自动分派到 `FeedForward`/`SharedFeedForward`，处理 `MirrorBasis` 对应 null NN 的情况。

```java
static NeuralNetwork[] load(Basis[] aBasis, List aData) // 从 Map 列表加载 NN 数组

// === 参数/梯度协议 ===
abstract void mountCptrParameter(IDoubleOrFloatCPointer aPtr)
abstract int cptrParameterSize()
abstract void mountParameter(Vector aVec)
abstract int parameterSize()
abstract void initParameters()                   // Kaiming 均匀初始化
abstract void updateParameters()
abstract void requireGrad(int aNumThreads)
abstract void mountGradCptrParameter(int aThreadID, IDoubleOrFloatCPointer aPtr)
abstract void mountGradParameter(Vector aVec)
abstract void backwardParameter()

// === 缓存与代码生成 ===
abstract int forwardCacheSize()
abstract int backwardCacheSize()
abstract void updateGenMap(Map<String, Object> rGenMap, int aGenIdx)
abstract boolean hasSameGenMap(NeuralNetwork aNN)
```
