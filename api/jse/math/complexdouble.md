# ComplexDouble

> `jse.math.ComplexDouble`

**核心职能**：低频复数值实现，`extends AbstractSettableComplexDouble`，`final`。`public` 字段 `mReal/mImag` 可直接读写，覆写算术运算。`new ComplexDouble(real, imag)` / `new ComplexDouble(IComplexDouble)`。

```java
// 字段（可直接读写）
double mReal, mImag

// 构造器
ComplexDouble(double aReal, double aImag)
ComplexDouble(double aReal)                 // imag=0.0
ComplexDouble()                             // (0,0)
ComplexDouble(IComplexDouble)               // 从接口拷贝
ComplexDouble(ComplexDouble)                // 直接字段拷贝

// 覆写全部方法（直接操作 mReal/mImag，比 default 更高效）
double real() / imag()
void setReal/setImag/setRealImag(double...)
ComplexDouble plus/minus/lminus/multiply/div/ldiv(double,double)  // 返回新对象
void plus2this/minus2this/... (double,double)                     // 原地修改
ComplexDouble negative() / conj()
double norm() / phase()
```
