# BoxPrism

> `jse.atom.BoxPrism`

**核心职能**：`implements IBox`，`final`。通用三斜模拟盒，isPrism=true，创建时预计算逆矩阵缓存加速 toDirect()。`new BoxPrism(IXYZ a, IXYZ b, IXYZ c)` / `new BoxPrism(ax,ay,az,bx,by,bz,cx,cy,cz)`。

```java
BoxPrism(IXYZ aA, IXYZ aB, IXYZ aC)      // 三个基向量（值拷贝，需右手系）
BoxPrism(double ax,ay,az, bx,by,bz, cx,cy,cz)  // 9 分量直接指定

// IBox 实现（返回全部 9 分量）
double ax/ay/az(), bx/by/bz(), cx/cy/cz()
boolean isPrism()             // true
boolean isLmpStyle()          // false（显式覆写）
BoxPrism copy()
double volume()               // A·(B×C) mixed product
void toDirect(XYZ)            // 使用缓存逆矩阵（创建时预计算）
```
