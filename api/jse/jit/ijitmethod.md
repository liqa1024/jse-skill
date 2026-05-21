# IJITMethod

> `jse.jit.IJITMethod`

**核心职能**：extends IPointer。编译后的单个 C 函数句柄。`invoke` 传入输入/输出原始指针（`IPointer.ptr_()`），返回 `int` 状态码。

```java
@UnsafeJNI int invoke(IPointer aDataIn, IPointer rDataOut)  // 调用 JIT 函数
```
