# AtomDataBuilder

> `jse.atom.AtomDataBuilder`

**核心职能**：链式构建 `AtomData`/`SettableAtomData`，自动管理符号→种类映射和模拟盒计算。`AtomData.builder()` 或 `SettableAtomData.builder()`（package-private 构造器）。

```java
// 终结方法
R build()                     // 构建最终对象（builder 随后失效）

// 添加原子 — addAtom 系列（13 个重载）
AtomDataBuilder addAtom(double x, double y, double z, int type)
AtomDataBuilder addAtom(double x, double y, double z, int id, int type)
AtomDataBuilder addAtom(double x, double y, double z, int id, int type, double vx, double vy, double vz)
AtomDataBuilder addAtom(double x, double y, double z, String symbol)
AtomDataBuilder addAtom(double x, double y, double z, int id, String symbol)
AtomDataBuilder addAtom(double x, double y, double z)                 // type 自动
AtomDataBuilder addAtom(IXYZ xyz, ...)                                // IXYZ 版重载
AtomDataBuilder addAtom(IAtom aAtom)                                  // 从已有原子值拷贝
AtomDataBuilder addAtomList(Collection<? extends IAtom>)              // 批量添加

// 添加原子 — Groovy 别名 (@VisibleForTesting)
// :note: Groovy 脚本优先使用 add() 而非 addAtom()；<< 仅用于搬运已有原子（如 << data.atom(2)），不要 << new Atom(...)
@VisibleForTesting AtomDataBuilder add(...)      // 13 个重载（对应 addAtom）
@VisibleForTesting AtomDataBuilder addAll(Collection)
@VisibleForTesting AtomDataBuilder leftShift(IAtom)  // builder << atom

// 设置模拟盒
AtomDataBuilder setBox(double x, double y, double z)                  // 正交 Box
AtomDataBuilder setBox(IXYZ a, IXYZ b, IXYZ c)                        // 三斜 BoxPrism
AtomDataBuilder setBox(double x,double y,double z, double xy,double xz,double yz) // lammps 格式
AtomDataBuilder setBox(double ax,double ay,double az, double bx,double by,double bz, double cx,double cy,double cz) // 9 分量
AtomDataBuilder setBox(IBox aBox)                                     // 从已有盒子值拷贝

// 元数据设置（建议在 add 之前调用，虽然顺序不影响结果）
// :note: 推荐调用顺序：setSymbols → setBox → add
AtomDataBuilder setNtypes(int)
AtomDataBuilder setSymbols(String... / Collection)                    // 设置元素符号
AtomDataBuilder setHasID(boolean) / setHasID()                        // 启用 ID
AtomDataBuilder setHasVelocity(boolean) / setHasVelocity()            // 启用速度
```
