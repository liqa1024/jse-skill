# ColumnMatrixFunc2

> `jse.math.function.ColumnMatrixFunc2`

> 此类标记为 @ApiStatus.Experimental

**核心职能**：等间距二维函数骨架，内部存储 ColumnMatrix。继承 AbstractFunc2，实现 IEqualIntervalFunc2、IDataShell\<ColumnMatrix\>。两函数同网格（相同 x0、y0、dx、dy、Nx、Ny）时 data 可共享以实现批量运算加速。

```java
// === 构造器 ===
protected ColumnMatrixFunc2(double aX0, double aY0, double aDx, double aDy, ColumnMatrix aData)

// === IDataShell<ColumnMatrix> ===
final void setInternalData(ColumnMatrix aData)
final ColumnMatrix internalData()
final int internalDataSize()
final @Nullable ColumnMatrix getIfHasSameOrderData(Object aObj)

// === 函数数据访问 ===
final IVector x()
final IVector y()
final ColumnMatrix f()

// === 索引访问 ===
final double get(int aI, int aJ)
final void set(int aI, int aJ, double aV)
int getINear(double aX)
int getJNear(double aY)

// === 等间距坐标 ===
final int Nx()
final int Ny()
final double x0()
final double dx()
final double y0()
final double dy()
final double getX(int aI)
final double getY(int aJ)
final void setX0(double aNewX0)
final void setY0(double aNewY0)

// === 单元素操作 ===
final void update(int aI, int aJ, DoubleUnaryOperator aOpt)
final double getAndUpdate(int aI, int aJ, DoubleUnaryOperator aOpt)

// === 拷贝与运算器 ===
final ColumnMatrixFunc2 copy()

protected class ColumnMatrixFunc2Operation_ extends ColumnMatrixFunc2Operation {
    protected ColumnMatrixFunc2 thisFunc2_()
    protected ColumnMatrixFunc2 newFunc2_()
}

final IFunc2Operation operation()

// === 子类扩展点 ===
public abstract double subs(double aX, double aY)
protected abstract ColumnMatrixFunc2 newInstance_(double aX0, double aY0, double aDx, double aDy, ColumnMatrix aData)
```
