# GrowableFloatCPointer

> `jse.cptr.GrowableFloatCPointer`

**核心职能**：`extends FloatCPointer implements IGrowableDoubleOrFloatCPointer`。同 `GrowableDoubleCPointer`。

```java
@UnsafeJNI GrowableFloatCPointer(long aInitCount)
GrowableFloatCPointer()
long count() / void ensureCapacity(long)
```
