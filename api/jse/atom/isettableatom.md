# ISettableAtom

> `jse.atom.ISettableAtom`

**核心职能**：`extends IAtom, ISettableXYZ`。增加种类/id/速度设置和 Groovy 兼容访问器。

```java
// === 抽象方法（覆写返回类型为 ISettableAtom 以支持链式） ===
ISettableAtom setX(double aX)
ISettableAtom setY(double aY)
ISettableAtom setZ(double aZ)
ISettableAtom setType(int aType)

// === 批量设置 ===
ISettableAtom setXYZ(double,double,double)         // 覆写返回 ISettableAtom
ISettableAtom setXYZ(IXYZ)

// === 可选设置器（default 抛 UnsupportedOperationException） ===
ISettableAtom setID(int aID)
ISettableAtom setVx/setVy/setVz(double)
ISettableAtom setVxyz(double,double,double)        // 同时设 vx,vy,vz
ISettableAtom setVxyz(IXYZ)

// === Groovy 兼容 (@VisibleForTesting) ===
@VisibleForTesting double getX/getY/getZ()
@VisibleForTesting int getId() / getType()
@VisibleForTesting ISettableAtom setId(int)
@VisibleForTesting double getVx/getVy/getVz()
@VisibleForTesting IXYZ getVxyz()
```
