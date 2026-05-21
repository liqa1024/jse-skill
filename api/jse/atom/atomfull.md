# AtomFull

> `jse.atom.AtomFull`

**核心职能**：`extends AtomID`。包含 {x, y, z, id, type, vx, vy, vz} 的完整原子。`new AtomFull(x,y,z,id,type,vx,vy,vz)` / `new AtomFull(IAtom)` / `new AtomFull()`。

```java
// 新增 字段
double mVx, mVy, mVz   // 速度分量

// 构造器
AtomFull(double aX, double aY, double aZ, int aID, int aType, double aVx, double aVy, double aVz)
AtomFull(IAtom aAtom)  // 从 IAtom 拷贝全部信息
AtomFull()             // 全零, id=-1, type=1

// 覆写
double vx(), vy(), vz()
boolean hasVelocity()  // 始终 true
AtomFull copy()
AtomFull setVx/setVy/setVz(double)
AtomFull setVxyz(double,double,double) / setVxyz(IXYZ)
```
