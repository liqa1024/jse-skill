# AbstractResizableStroke

> `jse.plot.AbstractResizableStroke`

**核心职能**：`IResizableStroke` 的抽象骨架实现。委托 `mStroke` 内部 `Stroke` 对象，代理 `createStrokedShape` 方法。子类仅需重写 `getStroke(aSize)` 工厂方法。

```java
// === 字段 ===
protected @NotNull Stroke mStroke
protected double mSize

// === 构造 ===
protected AbstractResizableStroke(double aSize)

// === 尺寸 ===
double getSize()
void setSize(double aSize)

// === Stroke 委托 ===
Shape createStrokedShape(Shape p)

// === 子类重写 ===
protected abstract @NotNull Stroke getStroke(double aSize)
```
