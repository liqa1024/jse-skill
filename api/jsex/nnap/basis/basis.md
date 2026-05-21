# Basis

> `jsex.nnap.basis.Basis`

> 此类标记为 `@ApiStatus.Experimental @ApiStatus.Internal`

**核心职能**：所有 JIT 编译基组的抽象根类，`implements ISavable`。定义参数/梯度挂载协议（`mountCptrParameter`/`mountParameter`/`requireGrad`/`backwardParameter`）、缓存大小查询（`forwardCacheSize`/`backwardCacheSize`）和 JIT 代码生成接口（`updateGenMap`/`hasSameGenMap`）。通过 `load(List)` 静态工厂从 JSON Map 列表自动分派到具体子类。

```java
static Basis[] load(List aData)                  // 从 Map 列表加载基组数组（分派到 Chebyshev/Spherical/Merged/Mirror/Shared）

// === 参数/梯度协议 ===
void mountCptrParameter(IDoubleOrFloatCPointer aPtr)
int cptrParameterSize()
void mountCptrHyperParameter(IDoubleOrFloatCPointer aPtr)
int cptrHyperParameterSize()
void initParameters()                            // 随机初始化可训练参数
void mountParameter(Vector aVec)
int parameterSize()
void updateParameters()                          // 同步参数到 C 指针
void requireGrad(int aNumThreads)
void mountGradCptrParameter(int aThreadID, IDoubleOrFloatCPointer aPtr)
void mountGradParameter(Vector aVec)
void backwardParameter()                         // 反向同步梯度

// === 查询 ===
abstract double rcut()                           // 截断半径
abstract int size()                              // 基组输出维度
abstract int forwardCacheSize(int aNumNei)
abstract int backwardCacheSize(int aNumNei)
abstract int backwardBackwardCacheSize(int aNumNei)

// === JIT 代码生成 ===
abstract void updateGenMap(Map<String, Object> rGenMap, int aGenIdx)
abstract boolean hasSameGenMap(Basis aBasis)
```
