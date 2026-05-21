# IntCPointer

> `jse.cptr.IntCPointer`

**核心职能**：`extends CPointer`。对应 C 的 `int *`。提供 `fill`（IDataShell/int[]/IntCPointer/标量）、`parse2dest`、`get`/`getAt`/`set`/`putAt`。`asVec`→`RefIntVector`。

```java
@UnsafeJNI static IntCPointer malloc/calloc(long aCount)
long typeSize()                              // sizeof(int) (native)
@UnsafeJNI void fill(IDataShell<int[]>/int[]/IntCPointer/int)
@UnsafeJNI void parse2dest(IDataShell<int[]>/int[]/IntCPointer)
@UnsafeJNI int get() / getAt(long) / getAt(int)       // Groovy 兼容
@UnsafeJNI void set(int) / putAt(long, int) / putAt(int, int)
void next/previous/rightShift/leftShift(...)
IntCPointer plus/minus/copy()
@UnsafeJNI IIntVector asVec(int aSize)
@UnsafeJNI List<Integer> asList(int aSize)
```
