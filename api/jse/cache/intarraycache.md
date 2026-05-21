# IntArrayCache

> `jse.cache.IntArrayCache`

**核心职能**：专门针对 `int[]` 的全局静态缓存工具。被 `IntVectorCache` / `IntMatrixCache` 内部依赖。

```java
static void returnArray(int @NotNull[] aArray)
static int @NotNull[] getZeros(int aMinSize)
static int @NotNull[] getArray(int aMinSize)

static void returnArrayFrom(int aMultiple, IListGetter<int @NotNull[]> aArrayGetter)
static void getZerosTo(int aMinSize, int aMultiple, IListSetter<int @NotNull[]> aZerosConsumer)
static void getArrayTo(int aMinSize, int aMultiple, IListSetter<int @NotNull[]> aArrayConsumer)
```
