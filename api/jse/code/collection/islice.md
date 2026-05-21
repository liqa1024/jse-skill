# ISlice

> `jse.code.collection.ISlice`

**核心职能**：定义索引重映射协议——将逻辑索引 `get(i)` 映射到物理索引。含 `of(...)` 静态工厂创建实例。

```java
int get(int aIndex)
int size()
static ISlice of(int... aIndices)
```
