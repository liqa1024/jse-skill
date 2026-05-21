# Atom

> `jse.atom.Atom`

**核心职能**：`extends AbstractSettableAtom`。包含 {x, y, z, type} 的最简原子实现，字段 public 可直接读写。`new Atom(x,y,z,type)` / `new Atom(x,y,z)`(type=1) / `new Atom()`(0,0,0,1) / `new Atom(IXYZ,type)` / `new Atom(IAtom)`(拷贝)。

```java
// 字段（可直接读写）
double mX, mY, mZ       // 笛卡尔坐标
int mType                // 种类编号

// 构造器
Atom(double aX, double aY, double aZ, int aType)
Atom(double aX, double aY, double aZ)            // type=1
Atom()                                           // (0,0,0) type=1
Atom(IXYZ aXYZ, int aType)
Atom(IXYZ aXYZ)                                  // type=1
Atom(IAtom aAtom)                                // 从已有原子拷贝

// IAtom/ISettableAtom 实现
double x(), y(), z()                             // → mX, mY, mZ
int type()                                       // → mType
Atom copy()                                      // 深拷贝
Atom setX/setY/setZ(double)                      // 返回 this 链式
Atom setXYZ(double,double,double) / setXYZ(IXYZ)
Atom setType(int)
final int index()                                // 永远返回 -1
final boolean hasIndex()                         // 永远返回 false
// 继承 IAtom default: id()=-1, hasID()=false, vx/vy/vz()=0, hasVelocity()=false ...
```
