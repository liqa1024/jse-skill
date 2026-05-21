# IFunc1

> `jse.math.function.IFunc1`

**核心职能**：一维函数核心接口。提供网格数据的索引存取、坐标转换、单元素更新、批量填充与遍历、算术运算，以及微分积分等操作。`IFunc1Subs` 详见 [ifunc1subs.md](ifunc1subs.md)。

```java
// 数据访问
IVector x()
IVector f()
double get(int aI)
double getNear(double aX)

// 数据修改
void set(int aI, double aV)
void setNear(double aX, double aV)

// 批量修改
// :note: Groovy 中列表直接匹配 Iterable 重载，无需 as double[] 强转
void fill(double[] aData)
void fill(double aValue)
void fill(IVector aVector)
void fill(IFunc1 aFunc1)
void fill(IFunc1Subs aFunc1Subs)
void fill(Iterable<? extends Number> aList)
void assign(DoubleSupplier aSup)
void forEach(DoubleConsumer aCon)

// 索引与坐标转换
int Nx()
double x0()
double dx(int aI)
double getX(int aI)
int getINear(double aX)
void setX0(double aNewX0)

// 单元素更新
void update(int aI, DoubleUnaryOperator aOpt)
double getAndUpdate(int aI, DoubleUnaryOperator aOpt)
void updateNear(double aX, DoubleUnaryOperator aOpt)
double getAndUpdateNear(double aX, DoubleUnaryOperator aOpt)

// 拷贝与运算器
IFunc1 copy()
IFunc1Operation operation()

// :note: Groovy 脚本优先使用 f(x) 调用 / f[i] 索引运算符
// === Groovy 运算符重载与别名（@VisibleForTesting） ===
default double call(double aX)
default double getAt(int aI)
default void putAt(int aI, double aV)

// === 算术运算 — default 方法 ===
default IFunc1 plus(double aRHS)
default IFunc1 minus(double aRHS)
default IFunc1 multiply(double aRHS)
default IFunc1 div(double aRHS)
default IFunc1 mod(double aRHS)
default IFunc1 plus(IFunc1 aRHS)
default IFunc1 minus(IFunc1 aRHS)
default IFunc1 multiply(IFunc1 aRHS)
default IFunc1 div(IFunc1 aRHS)
default IFunc1 mod(IFunc1 aRHS)
default void plus2this(double aRHS)
default void minus2this(double aRHS)
default void multiply2this(double aRHS)
default void div2this(double aRHS)
default void mod2this(double aRHS)
default void plus2this(IFunc1 aRHS)
default void minus2this(IFunc1 aRHS)
default void multiply2this(IFunc1 aRHS)
default void div2this(IFunc1 aRHS)
default void mod2this(IFunc1 aRHS)
```
