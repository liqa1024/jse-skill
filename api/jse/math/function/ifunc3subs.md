# IFunc3Subs

> `jse.math.function.IFunc3Subs`

**核心职能**：三维函数求值 lambda 接口（@FunctionalInterface），作为 `IFunc3.fill(IFunc3Subs)` 的参数，支持 lambda 逐点填充。

```java
@FunctionalInterface
double subs(double aX, double aY, double aZ)                       // 函数求值 f(x,y,z)
```
