# GrowableIntCPointer

> `jse.cptr.GrowableIntCPointer`

**核心职能**：`extends IntCPointer implements IGrowableCPointer`。同 `GrowableDoubleCPointer`。

```java
@UnsafeJNI GrowableIntCPointer(long aInitCount)
GrowableIntCPointer()
long count() / void ensureCapacity(long)
```
