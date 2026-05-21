# JITLibHandle

> `jse.jit.JITLibHandle`

> 此类为 @ApiStatus.Internal / package-private

**核心职能**：`extends ReferenceChecker`。自动回收 `SimpleJIT.Engine` 加载的动态库 handle，及可能存在的非长期缓存库文件。GC 时执行 `freeLibrary0` 并清理临时目录。

```java
// === 构造器 ===
JITLibHandle(SimpleJIT.Engine, long aPtr, @Nullable String aDirToRemove)

// === 查询 ===
boolean isNull()

// === ReferenceChecker 接口实现 ===
protected void dispose_() throws IOException

// === native ===
private static native void freeLibrary0(long aLibHandle)
```
