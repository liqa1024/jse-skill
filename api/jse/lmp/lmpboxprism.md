# LmpBoxPrism

> `jse.lmp.LmpBoxPrism`

**核心职能**：`extends LmpBox`，`final`。LAMMPS 三斜盒，增加 `xy/xz/yz` 倾斜因子（对应 `bx()/cx()/cy()`）。`new LmpBoxPrism(xlo, xhi, ... xy, xz, yz)` / 通过 `LmpBox.of(IBox)` 多态返回。

```java
LmpBoxPrism(double aX, double aY, double aZ, double aXY, double aXZ, double aYZ)
LmpBoxPrism(double xlo, xhi, ylo, yhi, zlo, zhi, double xy, double xz, double yz)
// 覆写
boolean isPrism() → true           // 三斜盒
boolean isLmpStyle() → true        // 显式覆写为 true（LAMMPS 格式三斜盒标志，区别于 BoxPrism/VaspBoxPrism 的 false）
double bx() → xy; double cx() → xz; double cy() → yz
```
