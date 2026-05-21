# IEqualIntervalFunc3

> `jse.math.function.IEqualIntervalFunc3`

**核心职能**：等间距三维函数标记接口，继承 `IFunc3`。x/y/z 坐标等间距分布，`dx(int)/dy(int)/dz(int)` 返回统一步长 `dx()/dy()/dz()`。

```java
// 统一步长 —— x 方向
double dx()                                                         // x 方向全局统一步长
default double dx(int aI)                                           // 覆盖父接口：忽略索引，返回 dx()

// 统一步长 —— y 方向
double dy()                                                         // y 方向全局统一步长
default double dy(int aJ)                                           // 覆盖父接口：忽略索引，返回 dy()

// 统一步长 —— z 方向
double dz()                                                         // z 方向全局统一步长
default double dz(int aK)                                           // 覆盖父接口：忽略索引，返回 dz()
```
