# NewCollections

> `jse.code.collection.NewCollections`

**核心职能**：与 `AbstractCollections` 方法对应，但每次都创建新 `ArrayList` 或 `T[]`（值拷贝），适用于需要独立修改结果的场景。`protected` 构造器，静态工具类。

```java
// 所有方法与 AbstractCollections 同名同模式，但返回 ArrayList<T> 或 T[]（值拷贝）
static <T> ArrayList<T> nulls(int aSize)       // 填充 null
static <T> ArrayList<T> from(...)
static ArrayList<Integer> range(...)
static <R,T> ArrayList<R> map(...)
static <T> T[] mapArray(T[], IUnaryFullOperator<T,T>)
static <T> ArrayList<T> slice(...)
static <T> ArrayList<T> filter(...)
static IntVector/Vector filterInt(...)/filterDouble(...)  // 返回数学向量
static <T> T[]/ArrayList<T> merge(...)
```
