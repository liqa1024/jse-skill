# CharScanner

> `jse.code.io.CharScanner`

**核心职能**：从 `char[]` 高效解析数值，专为 JSON/配置文件扫描优化，修复了 `.123` 格式解析 bug。纯静态工具类。

```java
static boolean isDigit/isNumberDigit/isDecimalDigit/isDecimalChar(int c)
static boolean hasDecimalChar/isLong/isInteger(char[] digitChars, ...)
static int parseInt/parseIntFromTo/parseIntFromToIgnoreDot(boolean ignoreErr, boolean[] anyErr, char[], ...)
static long parseLong/parseLongFromTo/parseLongFromToIgnoreDot(boolean ignoreErr, boolean[] anyErr, char[], ...)
static float parseFloat/parseFloatFromTo(boolean ignoreErr, boolean[] anyErr, char[], ...)
static double parseDouble/parseDoubleFromTo(boolean ignoreErr, boolean[] anyErr, char[], ...)
static Number parseNumber/parseNumberFromTo(boolean ignoreErr, boolean[] anyErr, char[], ...)
static int skipWhiteSpace(char[] array, int index, int length)
```
