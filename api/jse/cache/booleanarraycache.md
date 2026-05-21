# BooleanArrayCache

> `jse.cache.BooleanArrayCache`

**核心职能**：专门针对 `boolean[]` 的全局静态缓存工具。被 `LogicalVectorCache` 内部依赖。

```java
static void returnArray(boolean @NotNull[] aArray)
static boolean @NotNull[] getZeros(int aMinSize)       // 全 false
static boolean @NotNull[] getArray(int aMinSize)

static void returnArrayFrom(int aMultiple, IListGetter<boolean @NotNull[]> aArrayGetter)
static void getZerosTo(int aMinSize, int aMultiple, IListSetter<boolean @NotNull[]> aZerosConsumer)
static void getArrayTo(int aMinSize, int aMultiple, IListSetter<boolean @NotNull[]> aArrayConsumer)
```
