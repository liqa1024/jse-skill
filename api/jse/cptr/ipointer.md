# IPointer

> `jse.cptr.IPointer`

**核心职能**：顶层指针抽象（`@ApiStatus.Experimental`）。`ptr_()` 返回内部 `long` 指针值（`@ApiStatus.Internal`）。提供 `default` 方法将指针强制转换为各类型指针（`as*Pointer`/`as*CudaPointer`），等价于 C 的类型转换。

```java
// --- 内部指针值 ---
@ApiStatus.Internal long ptr_()                     // 内部存储的 C 指针值
default boolean isNull()                            // 指针是否为空 (0 或 -1)

// --- 类型转换 (类似 C 强制类型转换) ---
default CPointer asCPointer()                       // → (char *)
default IntCPointer asIntCPointer()                 // → (int *)
default Int64CPointer asInt64CPointer()             // → (int64_t *)
default DoubleCPointer asDoubleCPointer()           // → (double *)
default FloatCPointer asFloatCPointer()             // → (float *)
default AnyCPointer asAnyCPointer()                 // → (void **)
default NestedIntCPointer asNestedIntCPointer()     // → (int **)
default NestedDoubleCPointer asNestedDoubleCPointer() // → (double **)

// --- CUDA 类型转换 ---
default CudaPointer asCudaPointer()
default IntCudaPointer asIntCudaPointer() / Int64CudaPointer asInt64CudaPointer()
default FloatCudaPointer asFloatCudaPointer() / DoubleCudaPointer asDoubleCudaPointer()
```
