# IComplexDouble

> `jse.math.IComplexDouble`

**核心职能**：定义复数的只读协议（`real/imag`），并提供全套复数算术运算 default 方法。无基底接口。

```java
// === 抽象方法 ===
double real()                                     // 实部
double imag()                                     // 虚部

// === 只读算术运算（全部返回新 ComplexDouble） ===
ComplexDouble plus(IComplexDouble/ComplexDouble/double real,double imag/double real)
ComplexDouble minus(...)                          // this - rhs
ComplexDouble lminus(...)                         // rhs - this
ComplexDouble multiply(double,double)             // (a+bi)(c+di) = (ac-bd)+(ad+bc)i
ComplexDouble div(double,double)                  // this / rhs
ComplexDouble ldiv(double,double)                 // rhs / this
ComplexDouble negative()                          // -this

// === 属性 ===
double norm()                                     // |z| = hypot(real, imag)
double phase()                                    // arg(z) = atan2(imag, real)
double abs() → norm()                             // matlab 兼容
double angle() → phase()                          // 别名
ComplexDouble conj()                              // 共轭 (real, -imag)
```
