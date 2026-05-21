# GrowableInt64CPointer

> `jse.cptr.GrowableInt64CPointer`

**核心职能**：`extends Int64CPointer implements IGrowableCPointer`。同 `GrowableDoubleCPointer`。

```java
@UnsafeJNI GrowableInt64CPointer(long aInitCount)
GrowableInt64CPointer()
long count() / void ensureCapacity(long)
```
