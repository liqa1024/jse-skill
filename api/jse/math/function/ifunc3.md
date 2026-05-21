# IFunc3

> `jse.math.function.IFunc3`

> 此类标记为 @ApiStatus.Experimental

**核心职能**：三维函数核心接口。提供三维网格数据的索引存取与坐标转换。无骨架实现类，无 operation() 实现。`IFunc3Subs` 详见 [ifunc3subs.md](ifunc3subs.md)。

```java
// 数据访问
IVector x()
IVector y()
IVector z()
IVector f()
double get(int aI, int aJ, int aK)

// 数据修改
void set(int aI, int aJ, int aK, double aV)

// 索引与坐标转换
int Nx()
int Ny()
int Nz()
double x0()
double y0()
double z0()
double dx(int aI)
double dy(int aJ)
double dz(int aK)
double getX(int aI)
double getY(int aJ)
double getZ(int aK)
void setX0(double aNewX0)
void setY0(double aNewY0)
void setZ0(double aNewZ0)

// 拷贝
IFunc3 copy()

// Groovy（@VisibleForTesting）
default double call(double aX, double aY, double aZ)
default IFunc3YZ_ getAt(int aI)

// === 内部接口（@ApiStatus.Internal）===
@ApiStatus.Internal interface IFunc3YZ_ {
    IFunc3Z_ getAt(int aJ)
}
@ApiStatus.Internal interface IFunc3Z_ {
    double getAt(int aK)
    void putAt(int aK, double aV)
}
```
