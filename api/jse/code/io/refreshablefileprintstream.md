# RefreshableFilePrintStream

> `jse.code.io.RefreshableFilePrintStream`

**核心职能**：支持 `\r` 回车符覆盖刷新的 PrintStream，继承 `java.io.PrintStream`。专用于进度条输出到文件。`new RefreshableFilePrintStream(String filePath)` 或 `new RefreshableFilePrintStream(String filePath, String encoding)`。
