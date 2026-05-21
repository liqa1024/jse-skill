# IBox

> `jse.atom.IBox`

**核心职能**：`extends IXYZ`（x→ax, y→by, z→cz）。定义模拟盒的只读协议，支持正交、三斜、lammps 风格三种模式，内置 PBC wrap 和 direct/cartesian 坐标变换。

```java
// === 抽象方法 ===
double ax()                     // 基向量 a 的 x 分量（= IXYZ.x()）
double by()                     // 基向量 b 的 y 分量（= IXYZ.y()）
double cz()                     // 基向量 c 的 z 分量（= IXYZ.z()）
IBox copy()                     // 深拷贝（覆写 IXYZ.copy 返回类型）

// === 盒子类型（default） ===
boolean isPrism()               // 是否三斜，默认 false
boolean isLmpStyle()            // 是否 lammps 风格，默认 true

// === 完整基向量（default，基于 ax/by/cz + 倾斜分量合成） ===
IXYZ a()                        // new XYZ(ax(), ay(), az())
IXYZ b()                        // new XYZ(bx(), by(), bz())
IXYZ c()                        // new XYZ(cx(), cy(), cz())
// 倾斜分量（正交盒默认 0.0）
double ay(), az()               // a.y, a.z
double bx(), bz()               // b.x, b.z
double cx(), cy()               // c.x, c.y

// === lammps 倾斜因子别名 ===
double xy() → bx()              // lammps xy 倾斜
double xz() → cx()              // lammps xz 倾斜
double yz() → cy()              // lammps yz 倾斜

// === 覆写 IXYZ（映射到盒子轴） ===
double x() → ax()
double y() → by()
double z() → cz()

// === 核心几何方法 ===
double volume()                 // 体积（lmp: x*y*z; 三斜: mixed product; 正交: x*y*z）
void wrapPBC(XYZ rXYZ)          // 将笛卡尔坐标绕回盒内（toDirect → mod → toCartesian）
void toCartesian(XYZ rDirect)   // fractional/direct 坐标 → 笛卡尔坐标
void toDirect(XYZ rCartesian)   // 笛卡尔坐标 → fractional/direct 坐标
```
