# AtomicParameterCalculator

> `jse.atom.AtomicParameterCalculator`

**核心职能**：`implements AutoCloseable`。jse 结构分析核心：RDF/结构因子/BOOP/近邻列表/固体检测，基于 NCL 算法 + ParforThreadPool。`APC.of(IAtomData)` / `APC.of(IAtomData, threadNum)`，构造器 package-private+@Deprecated，必须用静态工厂。

> **`APC`**（`final extends AtomicParameterCalculator`）为简短别名，类级别 `@VisibleForTesting`。构造器 private，对外使用 `APC.of()`。

```java
// 静态工厂（推荐）
static AtomicParameterCalculator of(IAtomData, int threadNum)
static AtomicParameterCalculator of(IAtomData)             // 单线程
static <T> T withOf(IAtomData, int, IUnaryFullOperator)    // try-with 自动关闭
static <T> T withOf(IAtomData, IUnaryFullOperator)

// 生命周期
void close()                    // 关闭并归还缓存
boolean isClosed()
int nthreads()
AtomicParameterCalculator setNthreads(int)

// 属性查询
int natoms() / natoms(int type)
int ntypes()
double unitLen()               // 平均原子间距
double volume() / rho() / rho(int type)
double birho(int typeA, int typeB)  // 双体密度相关系数

// 坐标/种类修改
void setAtomXYZ(int idx, IXYZ) / setAtomXYZ(int idx, double x, double y, double z)
void setAtomType(int idx, int type)

// === RDF（径向分布函数） ===
IFunc1 calRDF(int N, double rMax)         // 全局 RDF
IFunc1 calRDF(int N) / calRDF()           // 自动 rMax=min(box)/2
IFunc1 calRDF_AB(int typeA, int typeB, int N, double rMax)  // 分种类
IFunc1 calRDF_G(int N, double rMax, double sigma)           // 高斯展宽
IFunc1 calRDF_AB_G(int typeA, int typeB, ...)
List<IFunc1> calAllRDF_G(int N, double rMax, double sigma)  // 所有种类对

// === SF（结构因子） ===
IFunc1 calSF(int N, double qMax, double qMin)
IFunc1 calSF_AB(int typeA, int typeB, ...)
static IFunc1 RDF2SF(IFunc1 rdf, double rho, ...)           // RDF→SF 转换
static IFunc1 SF2RDF(IFunc1 sf, double rho, ...)            // SF→RDF 转换

// === BOOP（键角序参量） ===
IVector calBOOP(int l, double rNearest, int nnn)            // Ql 序参量
IVector calABOOP(int l, double rNearest, int nnn)           // 平均 Ql
IVector calBOOP_W(int l, double rNearest, int nnn)          // Wl 序参量
IVector calABOOP_W(int l, double rNearest, int nnn)         // 平均 Wl
IVector calBOOP_Q(int l, double rNearest, int nnn)          // Ql（别名）
IComplexMatrix calYlmMean(int l, double rNearest, int nnn)  // Ylm 球谐平均值

// === 固体检测 ===
ILogicalVector checkSolidConnectRatio6(int nnn, double rNearest, double threshold)
ILogicalVector checkSolidConnectRatio4(int nnn, double rNearest, double threshold)
@VisibleForTesting ILogicalVector checkSolidS6(...) / checkSolidS4(...)  // 别名

// === 近邻列表 ===
IntVector getNeighborList(int idx, double rMax, int nnn)
IntVector getNeighborList(int idx, double rMax)
IntVector getNeighborList(int idx)                   // rMax=2*unitLen, nnn=12
IntVector getNeighborList(IXYZ position, double rMax, int nnn)  // 空间点查询

// @ApiStatus.Internal（内部使用，不导出）
@ApiStatus.Internal ParforThreadPool pool_()
@ApiStatus.Internal NeighborListGetter nl_()
@ApiStatus.Internal IMatrix positions()
@ApiStatus.Internal IIntVector types()
@ApiStatus.Internal IntVector getNeighborList_(...)
@ApiStatus.Internal List<Vector> getFullNeighborList_(...)
```
