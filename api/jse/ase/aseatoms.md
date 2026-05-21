# AseAtoms

> `jse.ase.AseAtoms`

**核心职能**：`extends AbstractSettableAtomData`。将 ASE 的 `Atoms` 对象包装为 jse 的 `ISettableAtomData`。内部以矩阵形式缓存 positions/numbers/momenta 数据，支持 ASE 特有的 `info`/`arrays`/`calc.results` 键值系统。`AseAtoms.of(pyAtoms)` / `AseAtoms.of(IAtomData)` / `AseAtoms.read(file)`。

```java
// === 静态工厂 ===
static AseAtoms of(PyObject aPyAtoms) throws JepException           // 从 ASE Atoms 创建
static AseAtoms of(PyObject aPyAtoms, boolean aLimited) throws JepException
static AseAtoms of(IAtomData aAtomData)                             // 从 jse IAtomData 转换
static AseAtoms of(IAtomData aAtomData, String... aSymbols)         // 指定符号映射
static AseAtoms of(IAtomData aAtomData, Collection aSymbols)
static AseAtoms of_compat(Object aAnyData) throws JepException      // Python 兼容入口（PyObject/IAtomData 自动分派）
// 从文件读取（底层调用 ase.io.read）
static AseAtoms read(String aFilePath) throws JepException
static Object read(String aFilePath, Map<String, Object> aKWArgs) throws JepException // 支持多帧返回 List

// === 直接导出为 ASE 对象（内部使用，对外推荐 IAtomData.ase()） ===
@ApiStatus.Internal PyObject toPyObject() throws JepException
@ApiStatus.Internal PyObject toPyObject(boolean aLimited) throws JepException

// === 核心 IAtomData 实现 ===
ISettableAtom atom(int aIdx)        // 返回 AbstractSettableAtom_ 匿名实现
IBox box()                          // 模拟盒
int natoms() / ntypes()
boolean hasVelocity()               // momenta!=null
boolean hasSymbol()                 // numbers!=null
String symbol(int aType)            // 从原子序数查表
double mass(int aType)              // 从符号查 CS.MASS
boolean hasMass()                   // = hasSymbol()

// === 覆写 AbstractSettableAtomData ===
AseAtoms setNtypes(int)             // 可截断/扩容种类
AseAtoms setSymbolOrder(String...)  // 重新排列原子序数→种类映射
AseAtoms setSymbols(String...)      // 根据新符号更新 numbers 数组
AseAtoms setNoVelocity() / setHasVelocity()
// setBox/setBoxNormal/setBoxPrism 等继承自 AbstractSettableAtomData，内部自动维护 mCell

// === ASE 特有数据访问 ===
// -- 直接获取底层矩阵 --
IIntVector atomicNumbers()          // 原子序数向量 (= numbers)
IMatrix positions()                 // 位置矩阵 (natoms × 3)
@Nullable IMatrix momenta()         // 动量矩阵 (natoms × 3)，无动量时 null
// -- 等效别名 (@VisibleForTesting) --
@VisibleForTesting IBox cell()              // → box()
@VisibleForTesting IIntVector numbers()     // → atomicNumbers()

// === info 系统（全局键值对，写入 ASE Atoms.info） ===
boolean hasInfo(String aKey)
@Unmodifiable Map<String,Object> infos()
Object info(String aKey)
AseAtoms setInfo(String aKey, Object aValue)    // value=null 时删除
Object removeInfo(String aKey)

// === arrays 系统（per-atom 键值对，写入 ASE Atoms.arrays） ===
// 支持类型: IVector/IIntVector/ILogicalVector/IMatrix/IIntMatrix/ILogicalMatrix/String[]/String[][]/NDArray/PyObject/List
boolean hasArray(String aKey)
@Unmodifiable Map<String,Object> arrays()
Object array(String aKey)
AseAtoms setArray(String aKey, Object aValue)   // 自动校验维度和类型
Object removeArray(String aKey)

// === calc.results 系统（计算结果键值对） ===
// 支持类型: double/IVector/IMatrix（按具体计算类型校验）
boolean hasCalcResult(String aKey)
@Unmodifiable Map<String,Object> calcResults()
Object calcResult(String aKey)
AseAtoms setCalcResult(String aKey, Object aValue) // 严格校验 energy/forces/stress 等特殊 key
Object removeCalcResult(String aKey)

// === 文件 I/O ===
void write(String aFilePath) throws JepException
void write(String aFilePath, Map<String, Object> aKWArgs) throws JepException
AseAtoms copy()

// === 常量 ===
final static double ASE_VEL_MUL  // ASE 速度单位转换系数
```
