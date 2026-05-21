# FloatCPointer

> `jse.cptr.FloatCPointer`

**核心职能**：`extends CPointer implements IDoubleOrFloatCPointer`。与 `DoubleCPointer` 镜像，元素类型为 `float`。跨精度支持 `fillD`/`parse2destD`/`getD`/`setD`。`asVec(aSize)`→`RefFloatVector`。

```java
// 方法签名与 DoubleCPointer 镜像，double↔float 互换
@UnsafeJNI static FloatCPointer malloc/calloc(long aCount)
long typeSize()                              // sizeof(float) (native)
@UnsafeJNI void fill(IDataShell<float[]>/float[]/FloatCPointer/float)
@UnsafeJNI void parse2dest(IDataShell<float[]>/float[]/FloatCPointer)
@UnsafeJNI float get() / getAt(long)
@UnsafeJNI void set(float) / putAt(long, float)
@UnsafeJNI float getF() / double getD()
@UnsafeJNI void setF(float) / setD(double)
FloatCPointer plus/minus/copy()
@UnsafeJNI IFloatVector asVec(int aSize)
@UnsafeJNI List<Float> asList(int aSize)
```
