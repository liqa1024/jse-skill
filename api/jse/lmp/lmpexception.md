# LmpException

> `jse.lmp.LmpException`

**核心职能**：`extends Exception`，`final`。LAMMPS 操作异常，构造时自动去除消息末尾的 LAMMPS 换行符。`new LmpException("error message")`。

```java
LmpException(String message)     // 自动 stripTrailing
```
