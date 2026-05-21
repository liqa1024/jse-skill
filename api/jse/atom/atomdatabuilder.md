# AtomDataBuilder

> `jse.atom.AtomDataBuilder`

**核心职能**：链式构建 `AtomData`/`SettableAtomData`，自动管理符号→种类映射和模拟盒计算。`AtomData.builder()` 或 `SettableAtomData.builder()`（package-private 构造器）。

```java
// 终结方法
R build()                     // 构建最终对象（builder 随后失效）

// 添加原子 — addAtom 系列（13 个重载）
void addAtom(double x, double y, double z, int type)
void addAtom(double x, double y, double z, int id, int type)
void addAtom(double x, double y, double z, int id, int type, double vx, double vy, double vz)
void addAtom(double x, double y, double z, String symbol)
void addAtom(double x, double y, double z, int id, String symbol)
void addAtom(double x, double y, double z)                 // type 自动
void addAtom(IXYZ xyz, ...)                                // IXYZ 版重载
void addAtom(IAtom aAtom)                                  // 从已有原子值拷贝
void addAtomList(Collection<? extends IAtom>)              // 批量添加

// 添加原子 — Groovy 别名 (@VisibleForTesting)
// :note: Groovy 脚本优先使用 << 运算符 / add() 追加
@VisibleForTesting void add(...)      // 13 个重载（对应 addAtom）
@VisibleForTesting void addAll(Collection)
@VisibleForTesting void leftShift(IAtom)  // builder << atom

// 设置模拟盒
void setBox(double x, double y, double z)                  // 正交 Box
void setBox(IXYZ a, IXYZ b, IXYZ c)                        // 三斜 BoxPrism
void setBox(double x,double y,double z, double xy,double xz,double yz) // lammps 格式
void setBox(double ax,double ay,double az, double bx,double by,double bz, double cx,double cy,double cz) // 9 分量
void setBox(IBox aBox)                                     // 从已有盒子值拷贝

// 元数据设置
void setNtypes(int)
void setSymbols(String... / Collection)                    // 设置元素符号
void setHasID(boolean) / setHasID()                        // 启用 ID
void setHasVelocity(boolean) / setHasVelocity()            // 启用速度
```
