# VaspBox

> `jse.vasp.VaspBox`

**核心职能**：`implements IBox`。VASP 风格的模拟盒——在正交 `IBox` 基础上增加晶格常数 `scale` 和 internal 坐标（i 前缀）。实际坐标 = internal × scale。`new VaspBox(ax, by, cz)` / `new VaspBox(ax, by, cz, scale)`。

```java
// 构造器
VaspBox(double aIAx, double aIBy, double aICz, double aScale)
VaspBox(double aIAx, double aIBy, double aICz)          // scale=1.0

// === IBox 实现（实际坐标 = internal × scale） ===
double ax() → iax()*scale         // 同理 ay/az/bx/by/bz/cx/cy/cz
VaspBox copy()
boolean isPrism()                 // false
boolean isLmpStyle()              // true（继承 IBox 默认）
// 继承 IBox default: volume/wrapPBC/toCartesian/toDirect...

// === VASP 特有属性 ===
double iax()                      // internal a.x (= mIAx)
double iby()                      // internal b.y (= mIBy)
double icz()                      // internal c.z (= mICz)
double iay() → 0.0               // 正交盒倾斜分量为 0
double ibx() → 0.0               // （VaspBoxPrism 覆盖为非零）
// ... 9 个 i 前缀分量
IXYZ ia() / ib() / ic()          // internal 基向量
IMatrix iabc()                    // internal 基向量按行矩阵 (3×3)
IMatrix inviabc()                // iabc 的逆矩阵（用于 Cartesian↔Direct 转换）

// === 晶格常数 ===
double scale()                    // 当前晶格常数
VaspBox setScale(double)          // 设置并触发 onAnyChange_()
```
