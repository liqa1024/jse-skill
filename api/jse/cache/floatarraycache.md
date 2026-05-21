# FloatArrayCache

> `jse.cache.FloatArrayCache`

**核心职能**：专门针对 `float[]` 的全局静态缓存工具，结构与 `DoubleArrayCache` 一致。被 `FloatVectorCache` 内部依赖。

```java
static void returnArray(float @NotNull[] aArray)
static float @NotNull[] getZeros(int aMinSize)
static float @NotNull[] getArray(int aMinSize)

static void returnArrayFrom(int aMultiple, IListGetter<float @NotNull[]> aArrayGetter)
static void getZerosTo(int aMinSize, int aMultiple, IListSetter<float @NotNull[]> aZerosConsumer)
static void getArrayTo(int aMinSize, int aMultiple, IListSetter<float @NotNull[]> aArrayConsumer)
```
