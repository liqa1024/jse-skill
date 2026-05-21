# VaspBoxPrism

> `jse.vasp.VaspBoxPrism`

**核心职能**：`extends VaspBox`，`final`。VASP 三斜盒，创建时预计算缓存（cross products + volume + 逆矩阵），加速 toDirect()。`new VaspBoxPrism(iax,iay,iaz, ibx,iby,ibz, icx,icy,icz, scale)` / `new VaspBoxPrism(iax,...icz)`(scale=1)。

```java
// 构造器（9 分量 + 可选 scale）
VaspBoxPrism(double iax, double iay, double iaz,
                    double ibx, double iby, double ibz,
                    double icx, double icy, double icz, double aScale)
VaspBoxPrism(double iax,...icz)   // scale=1.0

// === 覆写 ===
boolean isPrism()                 // true
boolean isLmpStyle()              // false（显式覆写）
VaspBoxPrism copy()
// 9 个 i 前缀分量全部返回实际值（非 0）
double iay/iaz/ibx/ibz/icx/icy()

// === 缓存加速（创建时预计算） ===
void toDirect(XYZ rCartesian)     // 使用缓存逆矩阵，自动 snap 近整数值
// setScale() 自动触发 initCache_() 重建缓存
```
