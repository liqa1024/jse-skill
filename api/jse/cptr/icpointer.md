# ICPointer

> `jse.cptr.ICPointer`

**核心职能**：extends IPointer（`@ApiStatus.Experimental`）。定义 C 指针全生命周期：`free` 释放、`memcpy` 拷贝、`typeSize` 类型大小、指针算术（`next/previous`=++/--、`rightShift/leftShift`=±=N、`plus/minus`=±N 返回新指针）。

```java
// --- 生命周期 ---
@UnsafeJNI void free()                               // free(ptr), 空指针抛异常
@UnsafeJNI void memcpy2dest(ICPointer rDest, long aCount)  // memcpy(dest, this, n)
@UnsafeJNI void memcpy2this(ICPointer aSrc, long aCount)   // memcpy(this, src, n)
long typeSize()                                      // sizeof(type)

// --- 指针算术 ---
void next()                                          // ++ptr
void rightShift(long aCount)                         // ptr += N
ICPointer plus(long aCount)                          // 返回 ptr + N (新对象)
void previous()                                      // --ptr
void leftShift(long aCount)                          // ptr -= N
ICPointer minus(long aCount)                         // 返回 ptr - N (新对象)

ICPointer copy()                                     // 浅拷贝 (共享同一 C 指针)
```
