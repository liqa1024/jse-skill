# MPIException

> `jse.parallel.MPIException`

**核心职能**：`final class extends Exception`。封装 MPI 错误码 `mErrCode`，所有 MPI 操作在出错时抛出此异常。

```java
MPIException(int aErrCode, String aMessage)
final int mErrCode
```
