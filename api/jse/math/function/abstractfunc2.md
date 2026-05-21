# AbstractFunc2

> `jse.math.function.AbstractFunc2`

**核心职能**：二维函数抽象骨架。`abstract class implements IFunc2`。提供 `fill`、`update`/`getAndUpdate` 的批量操作默认实现，以及 `getNear`/`setNear`/`updateNear`/`getAndUpdateNear` 的邻近快捷方法。

```java
// === 批量赋值 ===
final void fill(double)
final void fill(IMatrix)
final void fill(IFunc2)
final void fill(IFunc2Subs)

// === 单元素更新 ===
void update(int, int, DoubleUnaryOperator)
double getAndUpdate(int, int, DoubleUnaryOperator)

// === 邻近快捷 ===
final double getNear(double, double)
final void setNear(double, double, double)
final void updateNear(double, double, DoubleUnaryOperator)
final double getAndUpdateNear(double, double, DoubleUnaryOperator)

// === 抽象方法（子类必须实现） ===
abstract double get(int, int)
abstract void set(int, int, double)
abstract int getINear(double)
abstract int getJNear(double)
```
