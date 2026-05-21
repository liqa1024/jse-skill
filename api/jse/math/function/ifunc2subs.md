# IFunc2Subs

> `jse.math.function.IFunc2Subs`

**核心职能**：二维函数求值 lambda 接口（@FunctionalInterface），作为 `IFunc2.fill(IFunc2Subs)` 的参数，支持 lambda 逐点填充。

```java
@FunctionalInterface
double subs(double aX, double aY)                                   // 函数求值 f(x,y)
```
