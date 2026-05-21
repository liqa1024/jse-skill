# NestedIntCPointer

> `jse.cptr.NestedIntCPointer`

**核心职能**：`extends AnyCPointer`。与 `NestedDoubleCPointer` 镜像，元素类型为 `int`。fill/parse2dest 支持 `RowIntMatrix`/`int[]`。`asMat`→`RefIntMatrix`。

```java
@UnsafeJNI static NestedIntCPointer malloc/calloc(long aCount)
@UnsafeJNI void fill(RowIntMatrix/IDataShell<int[]>/int[] aData, ...)
@UnsafeJNI void fill(int aValue, long aRowNum, long aColNum)
@UnsafeJNI void parse2dest(RowIntMatrix/IDataShell<int[]>/int[] rDest, ...)
@UnsafeJNI int getAt(long aRow, long aCol)
@UnsafeJNI void putAt(long aRow, long aCol, int aValue)
@UnsafeJNI IntCPointer get() / getAt(long) / getAt(int)
NestedIntCPointer plus/minus/copy()
@UnsafeJNI List<IntCPointer> asList(int)
@UnsafeJNI IIntMatrix asMat(int aRowNum, int aColNum)
```
