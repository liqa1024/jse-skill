# APC

> `jse.atom.APC`

**核心职能**：`@VisibleForTesting final class extends AtomicParameterCalculator`，类型别名。构造器 `private`，仅通过静态工厂使用。所有方法继承自 `AtomicParameterCalculator`。

> 此类标记为 @VisibleForTesting。Groovy 脚本中优先使用 `APC.of()` / `APC.withOf()`。

```java
static AtomicParameterCalculator of(IAtomData, int threadNum)
static AtomicParameterCalculator of(IAtomData)             // 单线程
static <T> T withOf(IAtomData, int, IUnaryFullOperator)    // try-with 自动关闭
static <T> T withOf(IAtomData, IUnaryFullOperator)
```
