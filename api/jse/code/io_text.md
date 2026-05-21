# IO.Text

> `jse.code.IO.Text`

**核心职能**：字符串格式转换、终端 ANSI 颜色、字符串切分与数值解析、JSON/YAML/TOML/XML 字符串序列化等纯文本操作。静态内部类，不实例化。

```java
// ===== 字符串流 =====
static BufferedReader toReader(CharSequence aStr)             // CharSequence 转 BufferedReader
static void eachLine(CharSequence aStr, Consumer<String> aCon) throws IOException
static void eachLine(CharSequence aStr, BiConsumer<String, Integer> aCon) throws IOException // 带行号(0-based)

// ===== 数组转换 =====
static String[] toArray(Collection<? extends CharSequence> aLines) // 字符串集合转 String[]

// ===== ANSI 终端样式 =====
static String percent(double aProb)   // 概率转百分比字符串 (如 "12.34%")
static String underline(String aStr)  // 下划线
static String bold(String aStr)       // 粗体
static String red(String aStr)        // 红色
static String green(String aStr)      // 绿色
static String yellow(String aStr)     // 黄色
static String blue(String aStr)       // 蓝色
static String purple(String aStr)     // 紫色
static String cyan(String aStr)       // 青色

// ===== 字符串重复 =====
static String repeat(char aChar, int aNum)
static String repeat(CharSequence aStr, int aNum)

// ===== 字符串转数值 =====
static double str2double(String aStr)                       // 字符串转 double（高性能 CharScanner）
static double str2double(boolean aIgnoreErr, String aStr)   // 忽略错误，失败返回 NaN
static Number str2number(String aStr)                       // 字符串转 Number（自动检测整数/小数）
static Number str2number(boolean aIgnoreErr, String aStr)   // 忽略错误，失败返回 null

// ===== 字符串转向量 =====
static Vector str2data(String aStr, int aLength)            // 按空格/逗号分割为 Vector（指定长度）
static Vector str2data(String aStr)                         // 自动长度
static Vector str2data(boolean aIgnoreErr, String aStr, int aLength)
static Vector str2data(boolean aIgnoreErr, String aStr)

// ===== 索引查找 =====
static int findNoBlankIndex(String aStr, int aStart)        // 找首个非空字符索引
static int findBlankIndex(String aStr, int aStart)          // 找首个空字符索引

// ===== 字符串判断 =====
static boolean isBlank(final CharSequence self)             // 是否为空或空白
static boolean containsIgnoreCase(final CharSequence self, final CharSequence searchString)

// ===== 行查找 =====
static int findLineContaining(List<String> aLines, int aStart, String aContainStr, boolean aIgnoreCase)
static int findLineContaining(List<String> aLines, int aStart, String aContainStr)
static @Nullable String findLineContaining(BufferedReader aReader, String aContainStr, boolean aIgnoreCase) throws IOException
static @Nullable String findLineContaining(BufferedReader aReader, String aContainStr) throws IOException
static @Nullable String findLineNoBlank(BufferedReader aReader) throws IOException

// ===== 字符串分割 =====
static String[] splitBlank(String aStr)                     // 按空格分割，忽略多余空格
static String[] splitComma(String aStr)                     // 按逗号分割，忽略多余空格
static String[] splitStr(String aStr)                       // 按空格或逗号分割
static String[] splitDot(String aStr)                       // 按点分割
static List<String> splitNodeList(String aRawNodeList)      // 拆分 SLURM 节点列表

// ===== JSON/YAML/TOML/XML 字符串序列化 =====
static Map<?, ?> json2map(@Language("JSON") String aText)
static List<?> json2list(@Language("JSON") String aText)
static String map2json(Map<?, ?> aMap)
static String list2json(List<?> aList)
static String map2json(Map<?, ?> aMap, boolean aPretty)
static String list2json(List<?> aList, boolean aPretty)
static Map<?, ?> yaml2map(@Language("YAML") String aText)
static List<?> yaml2list(@Language("YAML") String aText)
static String map2yaml(Map<?, ?> aMap)
static String list2yaml(List<?> aList)
static Map<?, ?> toml2map(@Language("TOML") String aText)
static List<?> toml2list(@Language("TOML") String aText)
static String map2toml(Map<?, ?> aMap)
static String list2toml(List<?> aList)
static Map<?, ?> xml2map(@Language("XML") String aText) throws Exception
static String map2xml(Map<?, ?> aMap)
```
