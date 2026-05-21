# IDoubleOrFloatCPointer

> `jse.cptr.IDoubleOrFloatCPointer`

**核心职能**：extends ICPointer（`@ApiStatus.Experimental`）。统一 double/float 指针的读写接口。提供 `fillD`/`fillF`、`parse2destD`/`parse2destF`、`getD`/`getF`、`setD`/`setF`、`getAtD`/`getAtF`、`putAtD`/`putAtF`。跨精度类型自动转换（如 `DoubleCPointer` 也可 `fillF`/`getF`）。

```java
// --- 填充 (Java→C) ---
@UnsafeJNI void fillD(IDataShell<double[]> aData)          // Vector/Matrix 数据 → C
@UnsafeJNI void fillF(IDataShell<float[]> aData)
@UnsafeJNI void fillD(double[] aData, int aStart, int aCount)
@UnsafeJNI void fillF(float[] aData, int aStart, int aCount)
@UnsafeJNI void fillD(DoubleCPointer aData, long aCount)   // C → C
@UnsafeJNI void fillF(FloatCPointer aData, long aCount)
@UnsafeJNI void fillD(double aValue, long aCount)           // 标量广播填充
@UnsafeJNI void fillF(float aValue, long aCount)

// --- 解析 (C→Java) ---
@UnsafeJNI void parse2destD(IDataShell<double[]> rDest)
@UnsafeJNI void parse2destF(IDataShell<float[]> rDest)
@UnsafeJNI void parse2destD(double[] rDest, int aStart, int aCount)
@UnsafeJNI void parse2destF(float[] rDest, int aStart, int aCount)
@UnsafeJNI void parse2destD(DoubleCPointer rDest, long aCount)
@UnsafeJNI void parse2destF(FloatCPointer rDest, long aCount)

// --- 解引用 ---
@UnsafeJNI double getD()                             // *ptr (double)
@UnsafeJNI float getF()                              // *ptr (float)
@UnsafeJNI double getAtD(long aIdx)                  // ptr[aIdx] (double)
@UnsafeJNI float getAtF(long aIdx)                   // ptr[aIdx] (float)

// --- 赋值 ---
@UnsafeJNI void setD(double aValue)                  // *ptr = v
@UnsafeJNI void setF(float aValue)
@UnsafeJNI void putAtD(long aIdx, double aValue)     // ptr[aIdx] = v
@UnsafeJNI void putAtF(long aIdx, float aValue)

// --- 覆写签名收紧 ---
void next/previous/rightShift/leftShift(...)
IDoubleOrFloatCPointer plus/minus(long aCount)
IDoubleOrFloatCPointer copy()
```
