# DumpXYZ

> `jse.atom.data.DumpXYZ`

**核心职能**：`extends AbstractListWrapper<DataXYZ, IAtomData, DataXYZ>`。多帧 ext-xyz 数据的容器，支持 `dump[i]` 索引访问、追加帧、从文件读取/写入、截取操作（cutFront/cutBack/step）。`DumpXYZ.read(file)` / `DumpXYZ.of(IAtomData)` / `DumpXYZ.zl()`。

```java
// === 静态工厂 ===
static DumpXYZ read(String filePath) throws IOException
static DumpXYZ read(BufferedReader) throws IOException
static DumpXYZ of(IAtomData)                          // 单帧
static DumpXYZ of(IAtomData, String... symbols)       // 指定符号
static DumpXYZ of(Iterable<? extends IAtomData>)      // 多帧
static DumpXYZ of(Collection<? extends IAtomData>)
static DumpXYZ zl()                                   // 空容器

// === 数据操作 ===
DumpXYZ append(IAtomData)                             // 添加一帧（值拷贝）
DumpXYZ appendAll(Collection<? extends IAtomData>)    // 批量添加
DumpXYZ appendFile(String filePath)                   // 从文件追加帧
DumpXYZ copy()                                        // 深拷贝

// === 截取操作 ===
DumpXYZ cutFront(int length)                          // 保留前 N 帧
DumpXYZ cutBack(int length)                           // 保留后 N 帧
DumpXYZ step(int step)                                // 等间距采样

// === 文件 I/O ===
void write(String filePath) throws IOException
void write(IO.IWriteln writer) throws IOException

// === Groovy 操作符支持（继承自 AbstractListWrapper） ===
// dump[i] 索引访问, dump << frame, dump << collection
```
