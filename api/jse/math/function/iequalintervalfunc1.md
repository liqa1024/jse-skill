# IEqualIntervalFunc1

> `jse.math.function.IEqualIntervalFunc1`

**核心职能**：等间距一维函数标记接口，继承 `IFunc1`。表示 x 坐标等间距分布，`dx(int)` 返回统一步长 `dx()`。

```java
// 统一步长
double dx()                                                         // 全局统一步长
default double dx(int aI)                                           // 覆盖父接口：忽略索引，返回 dx()
```
