# GrowableDoubleCPointer

> `jse.cptr.GrowableDoubleCPointer`

**核心职能**：`extends DoubleCPointer implements IGrowableDoubleOrFloatCPointer`。无初始值，扩容时不保留旧值。增长策略 `Math.max(aMinCount, oCount + (oCount>>1))`（1.5 倍）。

```java
@UnsafeJNI GrowableDoubleCPointer(long aInitCount)     // 初始容量构造
GrowableDoubleCPointer()                               // 空构造 (count=0)
long count()
void ensureCapacity(long aMinCount)          // 不足时 1.5x 扩容，释放旧内存
```
