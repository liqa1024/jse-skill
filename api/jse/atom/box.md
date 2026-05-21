# Box

> `jse.atom.Box`

**核心职能**：`implements IBox`，`final`。直角正交模拟盒，isPrism=false, isLmpStyle=true（继承 IBox 默认）。`new Box(x,y,z)` / `new Box(IXYZ)`。

```java
Box(double aX, double aY, double aZ)
Box(IXYZ aBox)                // 值拷贝

// IBox 实现
double ax() / by() / cz()     // 三边长度
boolean isPrism()             // false
boolean isLmpStyle()          // true（继承 IBox 默认）
Box copy()
double volume()               // x * y * z
// 继承 IBox default: a()/b()/c()/wrapPBC/toCartesian/toDirect/x()/y()/z()...
```
