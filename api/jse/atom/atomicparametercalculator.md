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
int natoms()                     // 原子总数
int natoms(int type)             // 指定种类原子数
int ntypes()
double unitLen()                 // 平均原子间距
double volume()
double rho()                     // 全局数密度
double rho(int type)             // 指定种类数密度
double birho(int typeA, int typeB)  // 双体密度相关系数

// 坐标/种类修改
void setAtomXYZ(int idx, IXYZ xyz)
void setAtomXYZ(int idx, double x, double y, double z)
void setAtomType(int idx, int type)

// === RDF（径向分布函数） ===
// :note: N 定义间隔 Δr = rMax/N，输出点数 RDF 为 N、SF/RDF2SF 为 N+1（后续可能统一）
IFunc1 calRDF(int N, double rMax)                               // 全局 RDF
IFunc1 calRDF(int N) / calRDF()                                 // 自动 rMax=min(box)/2
IFunc1 calRDF_AB(int typeA, int typeB, int N, double rMax)      // 分种类
IFunc1 calRDF_AB(int typeA, int typeB)                          // → N=1000,rMax=unitLen*6
IFunc1 calRDF_G(int N, double rMax, int sigmaMul)               // 高斯展宽
IFunc1 calRDF_G(int N, double rMax) / calRDF_G(int N) / calRDF_G()  // → sigmaMul=4,N=1000,rMax=unitLen*6
IFunc1 calRDF_AB_G(int typeA, int typeB, int N, double rMax, int sigmaMul)
IFunc1 calRDF_AB_G(int typeA, int typeB, int N, double rMax)          // → sigmaMul=4
IFunc1 calRDF_AB_G(int typeA, int typeB, int N) / calRDF_AB_G(int typeA, int typeB)
List<? extends IFunc1> calAllRDF_G(int N, double rMax, int sigmaMul)  // 所有种类对
List<? extends IFunc1> calAllRDF_G(int N, double rMax) / calAllRDF_G(int N) / calAllRDF_G()  // → sigmaMul=4,N=160,rMax=unitLen*6

// === SF（结构因子） ===
IFunc1 calSF(int N, double qMax, double qMin)
IFunc1 calSF(int N, double qMax)                               // → qMin = 2π/unitLen*0.6
IFunc1 calSF(int N) / calSF()
IFunc1 calSF_AB(int typeA, int typeB, int N, double qMax, double qMin)
IFunc1 calSF_AB(int typeA, int typeB, int N, double qMax)     // → qMin = 2π/unitLen*0.6
IFunc1 calSF_AB(int typeA, int typeB, int N) / calSF_AB(int typeA, int typeB)
static IFunc1 RDF2SF(IFunc1 rdf, double rho, int N, double qMax, double qMin)
static IFunc1 RDF2SF(IFunc1 rdf, double rho, int N, double qMax)  // → qMin 自动
static IFunc1 RDF2SF(IFunc1 rdf, double rho, int N) / RDF2SF(IFunc1 rdf, double rho)
static IFunc1 SF2RDF(IFunc1 sq, double rho, int N, double rMax, double rMin)
static IFunc1 SF2RDF(IFunc1 sq, double rho, int N, double rMax)    // → rMin 自动
static IFunc1 SF2RDF(IFunc1 sq, double rho, int N) / SF2RDF(IFunc1 sq, double rho)

// === BOOP（键角序参量） ===
IVector calBOOP(int l, double rNearest, int nnn)             // Ql 旋转不变量
IVector calBOOP(int l, double rNearest) / calBOOP(int l)     // → nnn=-1,rNearest=unitLen*R_NEAREST_MUL
IVector calBOOP3(int l, double rNearest, int nnn)            // Ŵl 三阶不变量
IVector calBOOP3(int l, double rNearest) / calBOOP3(int l)   // → nnn=-1,rNearest=unitLen*R_NEAREST_MUL
IVector calABOOP(int l, double rNearest, int nnn)            // 平均 Ql（Lechner-Dellago）
IVector calABOOP(int l, double rNearest) / calABOOP(int l)   // → nnn=-1,rNearest=unitLen*R_NEAREST_MUL
IVector calABOOP3(int l, double rNearest, int nnn)           // 平均 Ŵl（Lechner-Dellago）
IVector calABOOP3(int l, double rNearest) / calABOOP3(int l) // → nnn=-1,rNearest=unitLen*R_NEAREST_MUL
IComplexMatrix calYlmMean(int l, double rNearest, int nnn)   // Ylm 球谐平均值
IComplexMatrix calYlmMean(int l, double rNearest) / calYlmMean(int l)

// === 连接比例 / 固体检测 ===
IVector calConnectRatioBOOP(int l, double threshold, double rNearest, int nnn)       // |Sij|>threshold 占比（原始 Qlm）
IVector calConnectRatioABOOP(int l, double threshold, double rNearest, int nnn)      // 平均版（Lechner-Dellago → Ackland-Jones）
ILogicalVector checkSolidConnectRatio6(double threshold, double rNearest, int nnn)   // l=6 固体检测（threshold 默认 0.58）
ILogicalVector checkSolidConnectRatio6(double threshold, double rNearest) / checkSolidConnectRatio6(double) / checkSolidConnectRatio6()
ILogicalVector checkSolidConnectRatio4(double threshold, double rNearest, int nnn)   // l=4 固体检测（threshold 默认 0.50）
ILogicalVector checkSolidConnectRatio4(double threshold, double rNearest) / checkSolidConnectRatio4(double) / checkSolidConnectRatio4()
@VisibleForTesting ILogicalVector checkSolidS6(double threshold, double rNearest, int nnn)
@VisibleForTesting ILogicalVector checkSolidS6(double threshold, double rNearest) / checkSolidS6(double) / checkSolidS6()
@VisibleForTesting ILogicalVector checkSolidS4(double threshold, double rNearest, int nnn)
@VisibleForTesting ILogicalVector checkSolidS4(double threshold, double rNearest) / checkSolidS4(double) / checkSolidS4()

// === 近邻列表 ===
IntVector getNeighborList(int idx, double rMax, int nnn)
IntVector getNeighborList(int idx, double rMax)
IntVector getNeighborList(int idx)                   // rMax=2*unitLen, nnn=12
IntVector getNeighborList(IXYZ position, double rMax, int nnn)  // 空间点查询
List<Vector> getFullNeighborList(int idx, double rMax, int nnn) // [x,y,z,idx] 含 PBC 镜像
List<Vector> getFullNeighborList(int idx, double rMax) / getFullNeighborList(int idx)

// @ApiStatus.Internal（内部使用，不导出）
@ApiStatus.Internal ParforThreadPool pool_()
@ApiStatus.Internal NeighborListGetter nl_()
@ApiStatus.Internal IMatrix positions()
@ApiStatus.Internal IIntVector types()
@ApiStatus.Internal IntVector getNeighborList_(...)
@ApiStatus.Internal List<Vector> getFullNeighborList_(...)
```
