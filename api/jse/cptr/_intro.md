# `jse.cptr`

> C 指针 JNI 包装——将 C 指针（`double*`/`int*`/`void**` 等）包装为 Java 对象，提供 malloc/free/memcpy/指针算术/解引用/数组访问/批量 fill/parse2dest。统一使用 MiMalloc 加速。通过 `asVec`/`asMat`/`asList` 零拷贝转为 jse 向量/矩阵/列表引用视图。整个包标注 `@ApiStatus.Experimental`。

## 架构总览 (Architecture)

```
IPointer (@Experimental)
  → ICPointer → IDoubleOrFloatCPointer (@Experimental) → IGrowableDoubleOrFloatCPointer (@Experimental)
                → IGrowableCPointer

Pointer (final, implements IPointer)    — 简单指针包装
CPointer (implements ICPointer)         — 通用 C 指针基类, sizeof(char)=1
  → AnyCPointer                         — void** 嵌套指针
    → NestedDoubleCPointer              — double** 矩阵指针
    → NestedIntCPointer                 — int** 矩阵指针
  → DoubleCPointer + IDoubleOrFloatCPointer   — double* 指针
    → GrowableDoubleCPointer + IGrowableDoubleOrFloatCPointer
  → FloatCPointer + IDoubleOrFloatCPointer    — float* 指针
    → GrowableFloatCPointer + IGrowableDoubleOrFloatCPointer
  → IntCPointer                                — int* 指针
    → GrowableIntCPointer + IGrowableCPointer
  → Int64CPointer                              — int64_t* 指针
    → GrowableInt64CPointer + IGrowableCPointer
```
