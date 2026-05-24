# AbstractListWrapper

> `jse.code.collection.AbstractListWrapper`

**核心职能**：泛型类 `AbstractListWrapper<R, T, E>`，对内部 `List<E>` 做类型安全包装，自动将外部类型 `T` 转为内部类型 `E`，内部类型 `E` 转为输出类型 `R`。需继承并实现 `toInternal_` 和 `toOutput_`。

```java
protected abstract E toInternal_(T aValue)
protected abstract R toOutput_(E aValue)
// === List 接口 ===
R get(int aIdx)
int size()
boolean add(T aValue)
void add(int aIdx, T aValue)
boolean addAll(Collection<? extends T> aList)
boolean addAll(int aIdx, Collection<? extends T> aList)
R set(int aIdx, T aValue)
R remove(int aIdx)
void clear()
List<R> asList()
Iterator<R> iterator()

// === 便捷方法 ===
R removeLast()
R first()
R last()
AbstractListWrapper<R,T,E> append(T aValue)
AbstractListWrapper<R,T,E> appendAll(Collection<? extends T> aList)
// === Groovy 运算符重载 (@VisibleForTesting) ===
// :note: Groovy 脚本优先使用 list[i] / list[i]=val / << / collect 运算符
@VisibleForTesting R getAt(int aIdx)
@VisibleForTesting void putAt(int aIdx, T aValue)
@VisibleForTesting List<R> getAt(Range aRange)
@VisibleForTesting List<R> getAt(EmptyRange aRange)
@VisibleForTesting List<R> getAt(Collection aIndices)
@VisibleForTesting List<R> collect()
@VisibleForTesting <RR> List<RR> collect(IUnaryFullOperator<RR,R> aTransform)
@VisibleForTesting AbstractListWrapper<R,T,E> leftShift(T aValue)
@VisibleForTesting AbstractListWrapper<R,T,E> leftShift(Collection<? extends T> aList)
```
