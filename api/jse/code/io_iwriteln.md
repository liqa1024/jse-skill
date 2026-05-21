# IO.IWriteln

> `jse.code.IO.IWriteln`

**核心职能**：可自动换行的写入流功能接口，由 `IO.toWriteln()` 系列方法生成。通过 `IO.toWriteln(...)` 获取实现。

```java
void writeln(CharSequence aLine) throws IOException  // 写入一行并换行
default void close() throws IOException              // 关闭流（默认空实现）
```
