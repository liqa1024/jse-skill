# IEqualIntervalFunc2

> `jse.math.function.IEqualIntervalFunc2`

**核心职能**：等间距二维函数标记接口，继承 `IFunc2`。x/y 坐标等间距分布，`dx(int)/dy(int)` 返回统一步长 `dx()/dy()`。

```java
// 统一步长 —— x 方向
double dx()                                                         // x 方向全局统一步长
default double dx(int aI)                                           // 覆盖父接口：忽略索引，返回 dx()

// 统一步长 —— y 方向
double dy()                                                         // y 方向全局统一步长
default double dy(int aJ)                                           // 覆盖父接口：忽略索引，返回 dy()
```
