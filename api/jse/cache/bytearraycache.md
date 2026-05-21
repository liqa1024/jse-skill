# ByteArrayCache

> `jse.cache.ByteArrayCache`

**核心职能**：专门针对 `byte[]` 的全局静态缓存工具。内部使用 `ThreadLocal<NavigableMap<Integer, IObjectPool<byte[]>>>`，以数组长度为键值进行分级缓存。返回 **大于等于** 要求长度的数组。提供 `entryInvalid(Map.Entry, int)` 包级私有辅助方法（当缓存条目长度 > 16 且超过请求长度的 1.5 倍时视为无效，避免过大浪费），供所有 `*ArrayCache` 类复用。

```java
// --- 单数组操作 ---
static void returnArray(byte @NotNull[] aArray)       // 归还数组（按长度自动分类缓存）
static byte @NotNull[] getZeros(int aMinSize)          // 获取全零数组 [≥ 要求长度]
static byte @NotNull[] getArray(int aMinSize)          // 获取数组 [≥ 要求长度，不保证清零]

// --- 批量操作 (IListGetter / IListSetter) ---
static void returnArrayFrom(int aMultiple, IListGetter<byte @NotNull[]> aArrayGetter)    // 批量归还（不保证等长）
static void getZerosTo(int aMinSize, int aMultiple, IListSetter<byte @NotNull[]> aZerosConsumer)  // 批量获取全零数组
static void getArrayTo(int aMinSize, int aMultiple, IListSetter<byte @NotNull[]> aArrayConsumer)  // 批量获取数组
```
