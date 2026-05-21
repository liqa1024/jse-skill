# AtomID

> `jse.atom.AtomID`

**核心职能**：`extends Atom`。在 `Atom` 基础上增加 `id` 字段。`new AtomID(x,y,z,id,type)` / `new AtomID(IXYZ,id,type)` / `new AtomID(IAtom)` / `new AtomID()`。

```java
// 新增 字段
int mID                 // 原子 ID

// 构造器
AtomID(double aX, double aY, double aZ, int aID, int aType)
AtomID(IXYZ aXYZ, int aID, int aType)
AtomID(IAtom aAtom)    // 从 IAtom 拷贝（含 id）
AtomID()               // (0,0,0) id=-1, type=1

// 覆写
int id()               // → mID
boolean hasID()        // 始终 true
AtomID copy()
AtomID setID(int)
```
