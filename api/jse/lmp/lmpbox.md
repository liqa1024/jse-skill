# LmpBox

> `jse.lmp.LmpBox`

**核心职能**：`implements IBox`。LAMMPS 风格的正交盒，支持 `(xlo,xhi)` 边界对或直接边长两种构造方式，引入 LAMMPS 特有的 `xlo/xhi` 边界访问。`new LmpBox(xhi-xlo, ...)` / `new LmpBox(xlo, xhi, ...)` / `LmpBox.of(IBox)`。

```java
// 构造器
LmpBox(double aX, double aY, double aZ)                         // 边长（lo=0）
LmpBox(double xlo, double xhi, double ylo, double yhi, double zlo, double zhi) // 边界对
LmpBox(@NotNull IXYZ aBox) / LmpBox(@NotNull IXYZ lo, @NotNull IXYZ hi)

// IBox 实现
LmpBox copy()
final double ax() / by() / cz()          // xhi-xlo / yhi-ylo / zhi-zlo
boolean isPrism() → false                // 正交盒
boolean isLmpStyle() → true              // 继承 IBox 默认
final double xlo() / xhi() / ylo() / yhi() / zlo() / zhi()

// 静态转换工厂
static LmpBox of(IBox aBox)              // 将任意 IBox 转为 LmpBox
static LmpBox of(IXYZ aA, IXYZ aB, IXYZ aC)
```
