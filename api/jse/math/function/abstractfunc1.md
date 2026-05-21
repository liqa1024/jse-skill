# AbstractFunc1

> `jse.math.function.AbstractFunc1`

**核心职能**：一维函数抽象骨架。`abstract class implements IFunc1`。提供 `fill`/`assign`/`forEach`/`update` 的批量操作默认实现，以及 `getNear`/`setNear`/`updateNear`/`getAndUpdateNear` 的邻近快捷方法。

```java
// === 批量赋值 ===
final void fill(double)
final void fill(IVector)
final void fill(IFunc1)
final void fill(IFunc1Subs)
final void fill(Iterable<? extends Number>)
final void assign(DoubleSupplier)
final void forEach(DoubleConsumer)

// === 单元素更新 ===
void update(int, DoubleUnaryOperator)
double getAndUpdate(int, DoubleUnaryOperator)

// === 邻近快捷 ===
final double getNear(double)
final void setNear(double, double)
final void updateNear(double, DoubleUnaryOperator)
final double getAndUpdateNear(double, DoubleUnaryOperator)

// === 抽象方法（子类必须实现） ===
abstract double get(int)
abstract void set(int, double)
abstract int getINear(double)
```
