# VectorFunc1

> `jse.math.function.VectorFunc1`

> 此类标记为 @ApiStatus.Experimental

**核心职能**：等间距一维函数骨架，内部存储 Vector。继承 AbstractFunc1，实现 IEqualIntervalFunc1、IDataShell\<Vector\>。两函数同网格（相同 x0、dx、Nx）时 data 可共享以实现批量运算加速。

```java
// === 构造器 ===
protected VectorFunc1(double aX0, double aDx, Vector aData)
protected VectorFunc1(IVector aX, IVector aF)                      // 插值构造，支持不等距 X，精度受限于等距重采样

// === IDataShell<Vector> ===
final void setInternalData(Vector aData)
final Vector internalData()
final int internalDataSize()
final @Nullable Vector getIfHasSameOrderData(Object aObj)

// === 函数数据访问 ===
final IVector x()
final Vector f()

// === 批量修改 ===
final void fill(double[] aData)

// === 索引访问 ===
final double get(int aI)
final void set(int aI, double aV)
int getINear(double aX)

// === 等间距坐标 ===
final int Nx()
final double x0()
final double dx()
final double getX(int aI)
final void setX0(double aNewX0)

// === 单元素操作 ===
final void update(int aI, DoubleUnaryOperator aOpt)
final double getAndUpdate(int aI, DoubleUnaryOperator aOpt)

// === 拷贝与运算器 ===
final VectorFunc1 copy()

protected class VectorFunc1Operation_ extends VectorFunc1Operation {
    protected VectorFunc1 thisFunc1_()
    protected VectorFunc1 newFunc1_()
}

final IFunc1Operation operation()

// === 子类扩展点 ===
public abstract double subs(double aX)
protected abstract VectorFunc1 newInstance_(double aX0, double aDx, Vector aData)
```
