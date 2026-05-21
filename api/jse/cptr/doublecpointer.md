# DoubleCPointer

> `jse.cptr.DoubleCPointer`

**核心职能**：`extends CPointer implements IDoubleOrFloatCPointer`。对应 C 的 `double *`。提供 `fill`（IDataShell/double[]/DoubleCPointer/标量）、`parse2dest`、`get`/`getAt`/`set`/`putAt`。**跨精度**：`fillF`/`parse2destF`/`getF`/`setF` 全支持。`asVec(aSize)`→`RefVector` 零拷贝引用视图。

```java
@UnsafeJNI static DoubleCPointer malloc/calloc(long aCount)
long typeSize()                              // sizeof(double) (native)

// --- 填充 ---
@UnsafeJNI void fill(IDataShell<double[]> aData)       // jse Vector→C
@UnsafeJNI void fill(double[] aData, int aStart, int aCount)
@UnsafeJNI void fill(DoubleCPointer aData, long aCount) // memcpy
@UnsafeJNI void fill(double aValue, long aCount)        // 标量广播

// --- 解析 ---
@UnsafeJNI void parse2dest(IDataShell<double[]> rDest)
@UnsafeJNI void parse2dest(double[] rDest, int aStart, int aCount)
@UnsafeJNI void parse2dest(DoubleCPointer rDest, long aCount)

// --- 解引用/索引 ---
@UnsafeJNI double get()                                // *ptr
@UnsafeJNI double getAt(long aIdx)                     // ptr[aIdx] (含 int 重载)
@UnsafeJNI double getD() / float getF()
@UnsafeJNI double getAtD(long) / float getAtF(long)

// --- 赋值 ---
@UnsafeJNI void set(double aValue)
@UnsafeJNI void putAt(long aIdx, double aValue)        // 含 int 重载
@UnsafeJNI void setD(double) / setF(float)
@UnsafeJNI void putAtD(long, double) / putAtF(long, float)

// --- 指针算术 (覆写) ---
void next/previous/rightShift/leftShift(...)
DoubleCPointer plus/minus(long aCount) / copy()

// --- 视图 ---
@UnsafeJNI IVector asVec(int aSize)                    // → RefVector 零拷贝
@UnsafeJNI List<Double> asList(int aSize)              // → AbstractRandomAccessList
```
