# IFunc2

> `jse.math.function.IFunc2`

**核心职能**：二维函数核心接口。提供二维网格数据的索引存取、坐标转换、单元素更新、批量填充、算术运算等操作。`IFunc2Subs` 详见 [ifunc2subs.md](ifunc2subs.md)。

```java
// 数据访问
IVector x()
IVector y()
IMatrix f()
double get(int aI, int aJ)
double getNear(double aX, double aY)

// 数据修改
void set(int aI, int aJ, double aV)
void setNear(double aX, double aY, double aV)

// 批量修改
void fill(double aValue)
void fill(IMatrix aMatrix)
void fill(IFunc2 aFunc2)
void fill(IFunc2Subs aFunc2Subs)

// 索引与坐标转换
int Nx()
int Ny()
double x0()
double y0()
double dx(int aI)
double dy(int aJ)
double getX(int aI)
double getY(int aJ)
int getINear(double aX)
int getJNear(double aY)
void setX0(double aNewX0)
void setY0(double aNewY0)

// 单元素更新
void update(int aI, int aJ, DoubleUnaryOperator aOpt)
double getAndUpdate(int aI, int aJ, DoubleUnaryOperator aOpt)
void updateNear(double aX, double aY, DoubleUnaryOperator aOpt)
double getAndUpdateNear(double aX, double aY, DoubleUnaryOperator aOpt)

// 拷贝与运算器
IFunc2 copy()
IFunc2Operation operation()

// :note: Groovy 脚本优先使用 f(x,y) 调用 / f[i][j] 索引运算符
// === Groovy 运算符重载与别名（@VisibleForTesting） ===
default double call(double aX, double aY)
default IFunc2Y_ getAt(int aI)

// === 内部接口（@ApiStatus.Internal）===
@ApiStatus.Internal interface IFunc2Y_ {
    double getAt(int aJ)
    void putAt(int aJ, double aV)
}

// === 算术运算 — default 方法 ===
default IFunc2 plus(double aRHS)
default IFunc2 minus(double aRHS)
default IFunc2 multiply(double aRHS)
default IFunc2 div(double aRHS)
default IFunc2 mod(double aRHS)
default IFunc2 plus(IFunc2 aRHS)
default IFunc2 minus(IFunc2 aRHS)
default IFunc2 multiply(IFunc2 aRHS)
default IFunc2 div(IFunc2 aRHS)
default IFunc2 mod(IFunc2 aRHS)
default void plus2this(double aRHS)
default void minus2this(double aRHS)
default void multiply2this(double aRHS)
default void div2this(double aRHS)
default void mod2this(double aRHS)
default void plus2this(IFunc2 aRHS)
default void minus2this(IFunc2 aRHS)
default void multiply2this(IFunc2 aRHS)
default void div2this(IFunc2 aRHS)
default void mod2this(IFunc2 aRHS)
```
