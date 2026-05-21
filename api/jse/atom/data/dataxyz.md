# DataXYZ

> `jse.atom.data.DataXYZ`

**核心职能**：`extends AbstractSettableAtomData`。扩展 XYZ 原子数据格式（ext-xyz）的完整实现——读取/写入/转换单帧数据，支持注释、参数系统（key-value）、属性系统（per-atom key-value）、速度、符号映射。`DataXYZ.read(filePath)` / `DataXYZ.of(IAtomData)` / `DataXYZ.of(IAtomData, String... symbols)`。

```java
// === 静态工厂 ===
static DataXYZ read(String filePath) throws IOException
static DataXYZ read(BufferedReader) throws IOException
static DataXYZ of(IAtomData)                        // 从任意 IAtomData 转换
static DataXYZ of(IAtomData, String... symbols)     // 指定符号顺序

// === 核心数据接口（覆写 AbstractSettableAtomData） ===
ISettableAtom atom(int aIdx)    // 坐标/速度从内部矩阵读写
IBox box()                      // 模拟盒
int natoms() / ntypes()
boolean hasVelocity()           // 是否有速度列
boolean hasSymbol()             // 内部使用 symbols 数组
String symbol(int type)
boolean hasMass()               // = hasSymbol() → CS.MASS
double mass(int type)

// === 符号/种类管理 ===
DataXYZ setSymbolOrder(String... symbols)   // 设置符号顺序（不改变种类编号）
DataXYZ setSymbols(String... symbols)       // 设置符号映射（可能改变种类编号）
DataXYZ setNtypes(int)
DataXYZ setNoVelocity() / setHasVelocity()

// === 注释 ===
String comment()
DataXYZ setComment(String)
@VisibleForTesting String getComment()       // Java Bean 别名

// === 参数系统（全局 key-value，写入 XYZ 注释行） ===
boolean hasParameter(String key)
Object parameter(String key)
Map parameters()
DataXYZ setParameter(String key, Object value)
Object removeParameter(String key)

// === 属性系统（per-atom key-value，写入 XYZ 属性行） ===
boolean hasProperty(String key)
Object property(String key)
Map properties()
DataXYZ setProperty(String key, Object value)
Object removeProperty(String key)

// === 键名校验 ===
static boolean isInvalidKey(String)             // 检查 key 是否为非法 XYZ 键名
static boolean isInvalidPropertyKey(String)     // 检查 key 是否为非法属性键名

// === 文件 I/O ===
DataXYZ copy()
void write(String filePath) throws IOException
void write(IO.IWriteln writer) throws IOException
```
