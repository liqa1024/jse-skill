# FileEndException

> `jse.code.FileEndException`

**核心职能**：专门标记文件读取已结束的特殊 IOException，用于 Dump/Data 多帧读取时与常规 I/O 错误区分。标准异常实例化。标注 `@ApiStatus.Experimental`。

```java
FileEndException()                   // 无附加信息
FileEndException(String aMsg)        // 带描述信息
```
