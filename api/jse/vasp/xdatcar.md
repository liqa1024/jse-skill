# XDATCAR

> `jse.vasp.XDATCAR`

**核心职能**：`extends AbstractListWrapper<POSCAR, IAtomData, POSCAR>`。多帧 POSCAR 容器，支持按帧索引 `xdatcar[i]`、截取、追加。`XDATCAR.read(file)` / `XDATCAR.of(IAtomData)` / `XDATCAR.of(Iterable<IAtomData>)` / `XDATCAR.zl()`。

```java
// === 静态工厂 ===
static XDATCAR read(String filePath) throws IOException
static XDATCAR read(BufferedReader) throws IOException   // 多帧循环读取，遇 EOF 截断
static XDATCAR zl()                                      // 空容器
static XDATCAR of(IAtomData)                             // 单帧
static XDATCAR of(IAtomData, String... symbols)
static XDATCAR of(Iterable<? extends IAtomData>)         // 多帧
static XDATCAR of(Iterable, String...) / of(Iterable, IListGetter) // 多帧+符号
static XDATCAR of(Collection<? extends IAtomData>)       // Collection 版
static XDATCAR of(Collection, String...) / of(Collection, IListGetter)
static XDATCAR of(AbstractListWrapper<? extends IAtomData,?,?>) // 直接包装
// matlab 兼容
static XDATCAR of_compat(Object[] aAtomDataArray)
static XDATCAR of_compat(Object[], String... aSymbols)

// === 数据操作 ===
XDATCAR append(IAtomData)                                // 追加一帧
XDATCAR appendAll(Collection<? extends IAtomData>)       // 批量追加
XDATCAR appendFile(String filePath)                      // 从文件追加
XDATCAR leftShift(IAtomData/Collection)                  // Groovy << 操作符

// === 截取 ===
XDATCAR cutFront(int length)                             // 保留前 N 帧
XDATCAR cutBack(int length)                              // 保留后 N 帧
XDATCAR step(int aStep)                                  // 等间距采样

// === I/O ===
void write(String aFilePath) throws IOException
void write(IO.IWriteln) throws IOException
XDATCAR copy()
```
