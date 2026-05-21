# POSCAR

> `jse.vasp.POSCAR`

**核心职能**：`extends AbstractSettableAtomData`。VASP POSCAR 格式的完整实现——读取/写入/转换，支持 Direct/Cartesian 两种坐标模式、种类排序存储、Selective dynamics。`POSCAR.read(file)` / `POSCAR.of(IAtomData)` / `POSCAR.of(IAtomData, String... symbols)`。

```java
// === 静态工厂 ===
static POSCAR read(String filePath) throws IOException
static POSCAR read(BufferedReader) throws IOException
static POSCAR of(IAtomData aAtomData)                       // 自动符号
static POSCAR of(IAtomData aAtomData, String... aSymbols)   // 指定符号
static POSCAR of(IAtomData, boolean selectiveDynamics, String...)
static POSCAR of(IAtomData, Collection<? extends CharSequence>)
static POSCAR of(IAtomData, boolean, Collection)

// === 核心 IAtomData 实现 ===
ISettableAtom atom(int aIdx)        // 含 setType 时种类排序重排逻辑
VaspBox box()                       // 内部 VaspBox
int natoms() / ntypes()
boolean hasSymbol()                 // typeNames != null
String symbol(int aType)            // typeNames[aType-1]
double mass(int aType)              // 从符号查 CS.MASS
boolean hasMass()                   // = hasSymbol()

// === POSCAR 特有属性 ===
@Nullable String comment()          // 第一行注释
String @Nullable[] typeNames()      // 种类名称数组
IMatrix direct()                    // Direct/Cartesian 坐标矩阵
boolean isCartesian()               // 是否为 Cartesian 坐标
boolean isSelectiveDynamics()       // 是否开启 Selective dynamics
int natoms(int aType)               // 指定种类的原子数
int natoms(String aType)            // 按名称查原子数（支持同名多 key）
// 设置
POSCAR setComment(@Nullable String)
POSCAR setSelectiveDynamics(boolean)

// === 坐标模式转换 ===
POSCAR setCartesian()               // Direct → Cartesian（乘 box，自动 snap）
POSCAR setDirect()                  // Cartesian → Direct（除 box，自动 snap 近整数）

// === 覆写 AbstractSettableAtomData ===
POSCAR setNtypes(int)               // 截断/扩容种类（自动命名 T2,T3...）
POSCAR setSymbolOrder(String...)    // 重新排列种类顺序（内部重排坐标矩阵）
POSCAR setSymbols(String...)        // 设置种类名称
POSCAR setNoSymbol()                // 清除符号
// setBox/setBoxNormal/setBoxPrism 等继承自 AbstractSettableAtomData

// === 写入 ===
void write(String aFilePath) throws IOException
void write(IO.IWriteln) throws IOException
POSCAR copy()
```
