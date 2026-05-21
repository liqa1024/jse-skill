# UnicodeReader

> `jse.code.io.UnicodeReader`

**核心职能**：自动检测并剥离 BOM，识别 UTF-8/UTF-16BE/16LE/UTF-32BE/32LE 编码，回退到指定默认编码。继承 `java.io.Reader`。`new UnicodeReader(InputStream in, String defaultEnc)`。
