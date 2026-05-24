# jse — 通用输入输出

IO 负责普通文件、目录、配置文件、CSV 和轻量文本解析。

> **类引用**：`IO`=`jse.code.IO`，`IO.Text`=`jse.code.IO.Text`

## 核心取向

- 普通脚本优先使用 `IO.readAllLines` / `IO.readAllText` / `IO.write` / `IO.writeText`
- 写入默认 UTF-8 + LF，并自动创建不存在的父目录
- 路径支持 `~` 展开和 `/` 拼接
- `IO` 面向文件路径，`IO.Text` 面向已有字符串
- 原子结构、LAMMPS、VASP 等格式应使用专用类（详见 `atom2.md`），不手写解析

## 普通文件

jse 对于普通文件读写提供了通用方法：

```groovy
// 行文本
List<String> lines = IO.readAllLines("input.txt")
IO.write("output.txt", "第一行", "第二行")     // 可变参数

// 整段文本
String text = IO.readAllText("input.txt")
IO.writeText("output.txt", "不带换行的文本")

// 二进制
byte[] data = IO.readAllBytes("input.bin")
IO.write("output.bin", byteArray)

// 只看文件开头
List<String> head = IO.readLines("input.txt", 10)
```

> 注意 `IO.write(path, "line")` 自动追加换行；`IO.writeText(path, text)` 不追加换行。需要追加、覆盖等细节时查 `api/jse/code/io.md` 的 `OpenOption` 重载。

## 目录与路径

jse 提供了系统无关的目录操作包装方法，其中目录操作优先使用 Groovy 友好别名：

```groovy
IO.mkdir("path/to/dir")                        // 创建
IO.rmdir("path/to/dir")                        // 删除
IO.cpdir("source/dir", "target/dir")           // 复制

IO.exists("path")                              // 是否存在
IO.isfile("path")                              // 是否为文件
IO.isdir("path")                               // 是否为目录
String[] files = IO.list("path/to/dir")        // 列出内容
```

路径变换：

```groovy
String abs = IO.toAbsolutePath("~/data/file.txt")  // ~ 展开
String rel = IO.toRelativePath(abs)                // 转相对，\ 统一为 /
String name = IO.toFileName("/path/to/file.txt")   // "file.txt"
String parent = IO.toParentPath("/path/to/file.txt")
```

> jse 路径常量统一为的绝对路径，且目录统一以 `/` 结尾从而可直接 `DIR + "文件名"` 拼接。临时目录见 `util.md`。

## 配置文件

jse 支持 JSON / YAML / TOML / XML 格式的配置文件支持：

```groovy
// 文件 → 对象
Map<?, ?> config = IO.json2map("config.json")
Map<?, ?> params = IO.yaml2map("params.yaml")

// 对象 → 文件
IO.map2json(config, "output.json")
IO.map2yaml(config, "output.yaml")

// 带格式化
IO.map2json(config, "output.json", true)
```

`toml` / `xml` 为相同模式。字符串版本使用 `IO.Text.json2map` / `IO.Text.map2json` 等。

## CSV 与表格数据

jse 针对 csv 表格数据提供专门支持：

```groovy
// 有列名或列语义 → csv2table
Table table = IO.csv2table("data.csv")

// 纯数值矩阵 → csv2data
RowMatrix matrix = IO.csv2data("data.csv")

// 写已有 Table
IO.table2csv(table, "out.csv")

// 按列写多个序列
IO.cols2csv([xCol, yCol], "out.csv", "x", "y")

// 按行写二维数据（data2csv 还支持 vector / func1 等类型）
IO.data2csv(doubleMatrix, "out.csv", "col1", "col2", "col3")
```

`cols2csv` / `data2csv` / `rows2csv` 均有 `Iterable` 重载，Groovy 列表直接传入。

> jse 内置 csv 读取同时兼容逗号 `,` 和任意数空格 ` ` 分隔，写入统一使用 `,` 分隔。
> 
> `Table` / `RowMatrix` 的操作见 `math.md` / `math2.md`。


非标准分隔符或引号规则回退到通用 CSV：

```groovy
import org.apache.commons.csv.CSVFormat

List<String[]> rows = IO.csv2str("data.tsv", CSVFormat.TDF)
IO.str2csv(rows, "out.tsv", CSVFormat.TDF)
```

## 文本解析：IO.Text

定位为"已有字符串的小工具"，不追求覆盖完整文本处理能力：

```groovy
// 数值
double x = IO.Text.str2double("3.14")
Number num = IO.Text.str2number("1.5e-3")

// 向量（同时支持空格和分号分割）
Vector v = IO.Text.str2data("1.0 2.0 3.0 4.0")

// 分割
String[] parts = IO.Text.splitBlank("a  b\tc")
String[] parts = IO.Text.splitComma("a, b, c")

// 查找
int idx = IO.Text.findLineContaining(lines, 0, "target")

// 终端样式
println(IO.Text.red("错误"))          // 另有 green / yellow / blue / bold / underline
println(IO.Text.percent(0.1234d))    // "12.34%"
```

> IO.Text 也针对配置文件也提供 `json2map` / `map2json` 等格式的字符串版本，与文件版本命名对应。

## 其余工具

```groovy
// 文件复制 / 移动 / 删除
IO.copy("source.txt", "target.txt")
IO.copy(url, "downloaded.txt")                  // 也支持 URL
IO.move("old/path", "new/path")
IO.delete("file.txt")

// Zip
IO.zip2dir("archive.zip", "output/dir")
IO.dir2zip("source/dir", "archive.zip")
```

底层 Reader / Writer / Stream 接口（`IO.toReader` / `IO.toWriter` 等）存在，但一般脚本不优先使用；只在普通读写接口不适用时查 `api/jse/code/io.md`。
