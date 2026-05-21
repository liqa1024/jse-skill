# Thermo

> `jse.lmp.Thermo`

**核心职能**：`extends Table`。LAMMPS thermo 输出数据，支持从 log 文件自动合并多段 thermo 或从 csv 读取。`Thermo.read(logFile)` / `Thermo.readCSV(csvFile)` / `Thermo.fromTable(ITable)`。

> **`Log`**（final extends Thermo）为 `@VisibleForTesting` 别名。

```java
// === 静态工厂 ===
static Thermo read(String logFilePath) throws IOException    // 从 log 文件解析（自动合并多段）
static Thermo read(BufferedReader) throws IOException
static Thermo readCSV(String csvPath) throws IOException     // 从 csv 读取
static Thermo fromTable(ITable)                              // 从已有 ITable 创建
static Thermo of(ITable)                                     // fromTable 别名

// === 文件 I/O ===
void write(String csvPath) throws IOException                // 写入 csv
Thermo copy()
// 继承 Table: thermo["Step"], thermo.col("Step"), thermo.heads(), nrows(), thermo.asMatrix()...
```
