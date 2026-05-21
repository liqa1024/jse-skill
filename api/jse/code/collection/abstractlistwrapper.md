# AbstractListWrapper

> `jse.code.collection.AbstractListWrapper`

**核心职能**：对内部 `List<E>` 做类型安全包装，自动将外部类型 `T` 转为内部类型 `E`，内部类型 `E` 转为输出类型 `R`。需继承并实现 `toInternal_` 和 `toOutput_`。

```java
protected abstract E toInternal_(T aValue)
protected abstract R toOutput_(E aValue)
final R get/set/remove(int), add/addAll, clear, size, asList, iterator
final R removeLast/first/last
AbstractListWrapper<R,T,E> append(T)/appendAll(Collection) // 链式追加
// :note: Groovy 运算符重载
@VisibleForTesting R getAt(int aIdx)                                    // :note: Groovy 脚本优先使用 list[i] 运算符
// :note: Groovy 运算符重载
@VisibleForTesting void putAt(int aIdx, T aValue)                       // :note: Groovy 脚本优先使用 list[i]=val 运算符
// :note: Groovy 运算符重载
@VisibleForTesting AbstractListWrapper<R,T,E> leftShift(T aValue)       // :note: Groovy 脚本优先使用 << 运算符
// :note: Groovy 运算符重载
@VisibleForTesting <U> List<U> collect(Closure<U> aTransform)          // :note: Groovy 脚本优先使用 collect 闭包
```
