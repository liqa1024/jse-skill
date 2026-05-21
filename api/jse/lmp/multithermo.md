# MultiThermo

> `jse.lmp.MultiThermo`

**核心职能**：`extends AbstractListWrapper<ITable, ITable, ITable>`。多段 LAMMPS thermo 数据容器，支持从 log 文件读取多段、合并、逐段写入。`MultiThermo.read(logFile)` / `MultiThermo.readCSV(dir)` / `MultiThermo.zl()`。

> **`MultiLog`**（final extends MultiThermo）为 `@VisibleForTesting` 别名。

```java
// === 静态工厂 ===
static MultiThermo read(String logFilePath) throws IOException  // 从 log 解析所有段
static MultiThermo read(BufferedReader) throws IOException
static MultiThermo readCSV(String path) throws IOException      // 从 csv 文件/文件夹读取
static MultiThermo readCSV(String path, IFilter<String>)        // 自定义过滤
static MultiThermo zl()                                         // 空容器
static MultiThermo fromTable(ITable)                            // 单段
static MultiThermo fromTableList(Iterable<? extends ITable>)    // 多段 Iterable
static MultiThermo fromTableList(Collection<? extends ITable>)  // 多段 Collection

// === 数据操作 ===
MultiThermo append(ITable)                                      // 追加一段
MultiThermo appendAll(Collection<? extends ITable>)             // 批量追加
MultiThermo appendFile(String logFilePath) throws IOException   // 从 log 文件追加
MultiThermo appendCSV(String csvPath) throws IOException        // 从 csv 追加
MultiThermo leftShift(ITable)                                    // Groovy << 操作符
MultiThermo leftShift(Collection<? extends ITable>)             // Groovy << 批量

// === 合并 ===
Thermo merge()                                                   // 按行拼接所有段为单个 Thermo

// === 文件 I/O ===
void write(String dir) throws IOException                        // 写入 thermo-N.csv 到文件夹
MultiThermo copy()
```
