# ISettableXYZ

> `jse.atom.ISettableXYZ`

**核心职能**：`extends IXYZ`。增加原地修改能力（setter + 2this 系列）和 Groovy bean 访问器。

```java
// === 抽象方法（返回 this 支持链式调用） ===
ISettableXYZ setX(double aX)
ISettableXYZ setY(double aY)
ISettableXYZ setZ(double aZ)

// === 批量设置 ===
ISettableXYZ setXYZ(double aX, double aY, double aZ)  // 链式 setX.setY.setZ
ISettableXYZ setXYZ(IXYZ aXYZ)                         // 从 IXYZ 拷贝

// === Groovy bean 访问器 (@VisibleForTesting) ===
@VisibleForTesting double getX()  // 返回 x()
@VisibleForTesting double getY()  // 返回 y()
@VisibleForTesting double getZ()  // 返回 z()

// === 2this 系列 — 就地修改（void，不创建新对象） ===
void cross2this(IXYZ/XYZ/double,double,double)
void negative2this()
void abs2this()
void plus2this(IXYZ/XYZ/double,double,double)          // this += rhs
void plus2this(double aValue)                           // this += 标量
void mplus2this(IXYZ/XYZ/double,double,double,double)   // this += rhs * mul
void minus2this(IXYZ/XYZ/double,double,double)
void lminus2this(IXYZ/XYZ/double,double,double)         // this = rhs - this
void multiply2this(IXYZ/XYZ/double,double,double)
void div2this(IXYZ/XYZ/double,double,double)
void ldiv2this(IXYZ/XYZ/double,double,double)           // this = rhs / this
```
