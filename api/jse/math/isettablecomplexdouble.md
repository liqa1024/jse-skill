# ISettableComplexDouble

> `jse.math.ISettableComplexDouble`

**核心职能**：`extends IComplexDouble`。增加原地设置和 2this 系列原地算术运算。

```java
// === 抽象方法 ===
void setReal(double)                               // 设置实部
void setImag(double)                               // 设置虚部
void setRealImag(double, double)                   // 同时设置实虚部（default）
void setNormPhase(double norm, double phase)       // 按模+辐角设置（default）

// === Groovy 访问器 (@VisibleForTesting) ===
@VisibleForTesting double getReal() → real()
@VisibleForTesting double getImag() → imag()

// === 2this 系列 — 原地修改（void） ===
void plus2this/minus2this/lminus2this(IComplexDouble/ComplexDouble/double,double/double)
void multiply2this/div2this/ldiv2this(...)
void negative2this() / conj2this()
```
