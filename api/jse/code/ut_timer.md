# UT.Timer

> `jse.code.UT.Timer`

**核心职能**：计时与进度条——基于 FixedTimer 的 tic/toc 高精度计时，基于 ProgressBar 的命令行进度条及 Iterable 包装，支持 FANCY_ASCII/COLORFUL_UNICODE_BLOCK 样式。

```java
// 计时器
static void tic()                       // 重置计时器
static void toc()                       // 打印总计时（消息 "Total"）
static void toc(String aMsg)            // 打印指定消息的计时
static double toc(boolean aFlag)        // 返回计时值，秒（不打印）

// 进度条创建/初始化
static void progressBar(Map<?, ?> aArgs)// 用 Map 创建（支持 TaskName/InitialMax/Style/Consumer 等）
static void progressBar(String aName, long aN)
static void progressBar(long aN)
// 进度条步进
static void progressBar(@Nullable String aExtraMsg) // 前进一步并设置消息
static void progressBar()                           // 前进一步

// 进度条包装 Iterable
static Iterable<?> progressBarWrapper(Map<?, ?> aArgs)
static <T> Iterable<T> progressBarWrapper(String aName, Iterable<T> aUnderlying)
static <T> Iterable<T> progressBarWrapper(Iterable<T> aUnderlying)

// :note: @VisibleForTesting 快捷别名（Groovy 脚本中优先使用）
@VisibleForTesting static void pbar(Map<?, ?> aArgs)
@VisibleForTesting static void pbar(String aName, long aN)
@VisibleForTesting static void pbar(long aN)
@VisibleForTesting static void pbar(@Nullable String aExtraMsg)
@VisibleForTesting static void pbar()
@VisibleForTesting static Iterable<?> pbarw(Map<?, ?> aArgs)
@VisibleForTesting static <T> Iterable<T> pbarw(String aName, Iterable<T> aUnderlying)
@VisibleForTesting static <T> Iterable<T> pbarw(Iterable<T> aUnderlying)

// 进度条样式常量
static ProgressBarStyle FANCY_ASCII
static ProgressBarStyle COLORFUL_UNICODE_BLOCK
```
