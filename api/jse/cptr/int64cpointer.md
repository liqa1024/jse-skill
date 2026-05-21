# Int64CPointer

> `jse.cptr.Int64CPointer`

**核心职能**：`extends CPointer`。对应 C 的 `int64_t *`（Java `long`）。`asVec`→`RefLongVector`。

```java
@UnsafeJNI static Int64CPointer malloc/calloc(long aCount)
long typeSize()                              // sizeof(int64_t) (native)
@UnsafeJNI void fill(IDataShell<long[]>/long[]/Int64CPointer/long)
@UnsafeJNI void parse2dest(IDataShell<long[]>/long[]/Int64CPointer)
@UnsafeJNI long get() / getAt(long) / getAt(int)
@UnsafeJNI void set(long) / putAt(long, long) / putAt(int, long)
void next/previous/rightShift/leftShift(...)
Int64CPointer plus/minus/copy()
@UnsafeJNI ILongVector asVec(int aSize)
@UnsafeJNI List<Long> asList(int aSize)
```
