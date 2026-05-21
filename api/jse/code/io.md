# IO

> `jse.code.IO`

**核心职能**：面向 Groovy 脚本的统一文件 I/O 接口。基于字符串路径、自动创建缺失目录、统一 UTF-8 编码 + LF 换行符。静态工具类，不实例化。

```java
// ===== 文件写入 =====
// 多行写入，自动覆盖目标文件并递归创建父目录
static void write(String aFilePath, String... aLines) throws IOException
static void write(String aFilePath, Iterable<? extends CharSequence> aLines) throws IOException
// 单行写入，末尾自动添加换行符
static void write(String aFilePath, String aLine) throws IOException
// 二进制写入
static void write(String aFilePath, byte[] aData) throws IOException
// 以上四种的 OpenOption 变体
static void write(String aFilePath, String[] aLines, OpenOption... aOptions) throws IOException
static void write(String aFilePath, Iterable<? extends CharSequence> aLines, OpenOption... aOptions) throws IOException
static void write(String aFilePath, String aLine, OpenOption... aOptions) throws IOException
static void write(String aFilePath, byte[] aData, OpenOption... aOptions) throws IOException
// Path 版本（用于内部）
static void write(Path aPath, byte[] aData, OpenOption... aOptions) throws IOException
static void write(Path aPath, String aLine, OpenOption... aOptions) throws IOException
static void write(Path aPath, Iterable<? extends CharSequence> aLines, OpenOption... aOptions) throws IOException
// 写入文本字符串，末尾不加换行符
static void writeText(String aFilePath, String aText) throws IOException
static void writeText(String aFilePath, String aText, OpenOption... aOptions) throws IOException
static void writeText(Path aPath, String aText, OpenOption... aOptions) throws IOException

// ===== 文件读取 =====
static byte[] readAllBytes(String aFilePath) throws IOException      // 读取全部二进制
static List<String> readAllLines(String aFilePath) throws IOException // 读取全部行（自动忽略末尾单个换行符）
static List<String> readLines(String aFilePath, int aNumber) throws IOException // 读取指定行数
static List<String> readAllLines(BufferedReader aReader) throws IOException   // 从 Reader 读取全部行
static List<String> readLines(BufferedReader aReader, int aNumber) throws IOException // 从 Reader 读取指定行数
static String readAllText(String aFilePath) throws IOException       // 读取全部文本

// ===== 目录操作 =====
static void removeDir(String aDir) throws IOException     // 递归删除文件夹
static void copyDir(String aSourceDir, String aTargetDir) throws IOException // 递归复制文件夹
static void makeDir(String aDir) throws IOException       // 递归创建文件夹
static void makeDir(Path aDir) throws IOException         // Path 版本
static String @NotNull[] list(String aDir) throws IOException // 列出文件夹下文件名数组
// :note: @VisibleForTesting 别名（Groovy 脚本中优先使用）
@VisibleForTesting static void rmdir(String aDir) throws IOException
@VisibleForTesting static void cpdir(String aSourceDir, String aTargetDir) throws IOException
@VisibleForTesting static void mkdir(String aDir) throws IOException

// ===== 路径检测 =====
static boolean isDir(String aDir)                         // 判断是否为文件夹
static boolean isFile(String aFilePath)                   // 判断是否为文件
static boolean exists(String aPath)                       // 判断路径是否存在
static boolean isInternalValidDir(@NotNull String aDir)   // 路径是否符合 jse 内部格式（结尾有 / 或为空）
static String toInternalValidDir(@NotNull String aDir)    // 将路径转为 jse 内部格式（补结尾 /）
// :note: @VisibleForTesting 别名（Groovy 脚本中优先使用）
@VisibleForTesting static boolean isdir(String aDir)
@VisibleForTesting static boolean isfile(String aFilePath)

// ===== 复制/删除/移动 =====
static void delete(String aPath) throws IOException       // 删除文件或空文件夹
static void copy(String aSourcePath, String aTargetPath) throws IOException // 复制文件
static void copy(InputStream aSourceStream, String aTargetPath) throws IOException // 从流复制
static void copy(URL aSourceURL, String aTargetPath) throws IOException         // 从 URL 复制
static void copy(Path aSourcePath, Path aTargetPath) throws IOException         // Path 版本
static void copy(InputStream aSourceStream, Path aTargetPath) throws IOException
static void copy(URL aSourceURL, Path aTargetPath) throws IOException
static void move(String aSourcePath, String aTargetPath) throws IOException     // 移动文件或文件夹
static void move(Path aSourcePath, Path aTargetPath) throws IOException

// ===== 权限操作 =====
static void setExecutable(String aPath, boolean aExecutable) throws IOException
static void setExecutable(String aPath) throws IOException  // 设置可执行（默认 true）
static boolean isExecutable(String aPath)
static boolean isExecutable(Path aPath)

// ===== 文件映射（按行转换） =====
static void map(String aSourcePath, String aTargetPath,
    IUnaryFullOperator<? extends CharSequence, ? super String> aOpt) throws IOException
static void map(URL aSourceURL, String aTargetPath,
    IUnaryFullOperator<? extends CharSequence, ? super String> aOpt) throws IOException
static void map(BufferedReader aReader, IWriteln aWriter,
    IUnaryFullOperator<? extends CharSequence, ? super String> aOpt) throws IOException

// ===== 流获取（OutputStream / BufferedWriter / IWriteln） =====
static OutputStream toOutputStream(String aFilePath) throws IOException
static OutputStream toOutputStream(String aFilePath, OpenOption... aOptions) throws IOException
static OutputStream toOutputStream(Path aPath, OpenOption... aOptions) throws IOException
static BufferedWriter toWriter(String aFilePath) throws IOException
static BufferedWriter toWriter(String aFilePath, OpenOption... aOptions) throws IOException
static BufferedWriter toWriter(Path aPath, OpenOption... aOptions) throws IOException
static BufferedWriter toWriter(OutputStream aOutputStream)                 // 默认 UTF-8
static BufferedWriter toWriter(OutputStream aOutputStream, Charset aCS)
static IWriteln toWriteln(String aFilePath) throws IOException
static IWriteln toWriteln(String aFilePath, OpenOption... aOptions) throws IOException
static IWriteln toWriteln(Path aPath, OpenOption... aOptions) throws IOException
static IWriteln toWriteln(OutputStream aOutputStream)
static IWriteln toWriteln(OutputStream aOutputStream, Charset aCS)
static IWriteln toWriteln(BufferedWriter aWriter)

// ===== 流获取（InputStream / BufferedReader） =====
static InputStream toInputStream(String aFilePath) throws IOException
static InputStream toInputStream(Path aPath) throws IOException
static BufferedReader toReader(String aFilePath) throws IOException
static BufferedReader toReader(Path aPath) throws IOException
static BufferedReader toReader(URL aFileURL) throws IOException
static BufferedReader toReader(InputStream aInputStream) throws IOException         // 自动检测 BOM
static BufferedReader toReader(InputStream aInputStream, Charset aCS) throws IOException
static BufferedReader toReader(InputStream aInputStream, Charset aCS, boolean aUseUnicodeReader) throws IOException

// ===== 路径工具 =====
static File toFile(String aFilePath)                     // 字符串转 File
static void validPath(String aPath) throws IOException   // 合法化路径（自动创建父目录）
static void validPath(Path aPath) throws IOException
@ApiStatus.Internal static URL getResource(String aPath) // 获取 jar 包内 assets/ 路径下的资源 URL
static boolean samePath(String aPath1, String aPath2)    // 判断是否指向相同位置（基于字符串）
static @Nullable String toParentPath(String aPath)       // 获取父路径
static String toFileName(String aPath)                   // 获取文件名（最后一项）
static String toRelativePath(String aPath)               // 转为相对路径（同时 \ 统一替换为 /）
static String toAbsolutePath(String aPath)               // 转为绝对路径（支持 ~ 开头）
static boolean isAbsolutePath(String aPath)              // 判断是否为绝对路径
static boolean isAbsolutePath(Path aPath)

// ===== Zip 压缩/解压 =====
static void zip2dir(String aZipFilePath, String aDir) throws IOException  // 解压 zip
static void dir2zip(String aDir, String aZipFilePath, int aCompressLevel) throws IOException
static void dir2zip(String aDir, String aZipFilePath) throws IOException   // 默认压缩等级
static void files2zip(String[] aPaths, String aZipFilePath, int aCompressLevel) throws IOException
static void files2zip(String[] aPaths, String aZipFilePath) throws IOException
static void files2zip(Iterable<? extends CharSequence> aPaths, String aZipFilePath, int aCompressLevel) throws IOException
static void files2zip(Iterable<? extends CharSequence> aPaths, String aZipFilePath) throws IOException

// ===== JSON/YAML/TOML/XML 文件读写 =====
static Map<?, ?> json2map(String aFilePath) throws IOException
static List<?> json2list(String aFilePath) throws IOException
static void map2json(Map<?, ?> aMap, String aFilePath) throws IOException
static void list2json(List<?> aList, String aFilePath) throws IOException
static void map2json(Map<?, ?> aMap, String aFilePath, boolean aPretty) throws IOException
static void list2json(List<?> aList, String aFilePath, boolean aPretty) throws IOException
// YAML
static Map<?, ?> yaml2map(String aFilePath) throws IOException
static List<?> yaml2list(String aFilePath) throws IOException
static void map2yaml(Map<?, ?> aMap, String aFilePath) throws IOException
static void list2yaml(List<?> aList, String aFilePath) throws IOException
// TOML
static Map<?, ?> toml2map(String aFilePath) throws IOException
static List<?> toml2list(String aFilePath) throws IOException
static void map2toml(Map<?, ?> aMap, String aFilePath) throws IOException
static void list2toml(List<?> aList, String aFilePath) throws IOException
// XML
static Map<?, ?> xml2map(String aFilePath) throws Exception
static void map2xml(Map<?, ?> aMap, String aFilePath) throws Exception

// ===== CSV 写入 =====
// Groovy 中列表直接匹配 Iterable 重载，无需 as double[] / as double[][] 强转
// double[] — 单列
static void data2csv(double[] aData, String aFilePath) throws IOException
static void data2csv(double[] aData, String aFilePath, String aHead) throws IOException
// double[][] — 按行（data2csv 与 rows2csv 等价）
static void data2csv(double[][] aData, String aFilePath) throws IOException
static void data2csv(double[][] aData, String aFilePath, String... aHeads) throws IOException
static void rows2csv(double[][] aRows, String aFilePath) throws IOException
static void rows2csv(double[][] aRows, String aFilePath, String... aHeads) throws IOException
// double[][] — 按列
static void cols2csv(double[][] aCols, String aFilePath) throws IOException
static void cols2csv(double[][] aCols, String aFilePath, String... aHeads) throws IOException
// :note: Iterable — 按行（data2csv 与 rows2csv 等价，Groovy 首选）
static void data2csv(Iterable<?> aData, String aFilePath) throws IOException
static void data2csv(Iterable<?> aData, String aFilePath, String... aHeads) throws IOException
static void rows2csv(Iterable<?> aRows, String aFilePath) throws IOException
static void rows2csv(Iterable<?> aRows, String aFilePath, String... aHeads) throws IOException
// :note: Iterable — 按列（Groovy 首选）
static void cols2csv(Iterable<?> aCols, String aFilePath) throws IOException
static void cols2csv(Iterable<?> aCols, String aFilePath, String... aHeads) throws IOException
// IMatrix — 按行
static void data2csv(IMatrix aData, String aFilePath) throws IOException
static void data2csv(IMatrix aData, String aFilePath, String... aHeads) throws IOException
// IVector — 单列
static void data2csv(IVector aData, String aFilePath) throws IOException
static void data2csv(IVector aData, String aFilePath, String aHead) throws IOException
// IFunc1 — 输出两列：f（函数值）, x（自变量），默认头 "f,x"
static void data2csv(IFunc1 aFunc, String aFilePath) throws IOException
static void data2csv(IFunc1 aFunc, String aFilePath, String... aHeads) throws IOException
// ITable — 保留列头，按行写入
static void table2csv(ITable aTable, String aFilePath) throws IOException
// 通用 CSV（Apache Commons CSV，完整格式支持）
static void str2csv(Iterable<?> aLines, String aFilePath, CSVFormat aFormat) throws IOException
static void str2csv(Iterable<?> aLines, String aFilePath) throws IOException

// ===== CSV 读取 =====
static RowMatrix csv2data(String aFilePath) throws IOException   // 读取为矩阵（自动检测头行转为列数，返回 RowMatrix：nrows/ncols）
static Table csv2table(String aFilePath) throws IOException      // 读取为表格（保留列头，返回 Table：nrows/ncols/get(int row, String colName)）
static List<String[]> csv2str(String aFilePath, CSVFormat aFormat) throws IOException
static List<String[]> csv2str(String aFilePath) throws IOException

// ===== 其他 =====
@ApiStatus.Experimental
static void fileEnd(String aMsg) throws FileEndException  // STRICT_IO 模式下抛出 FileEndException
@ApiStatus.Experimental
static void fileEnd() throws FileEndException
```
