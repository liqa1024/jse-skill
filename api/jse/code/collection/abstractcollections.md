# AbstractCollections

> `jse.code.collection.AbstractCollections`

**核心职能**：基于视图模式创建不可变/可变集合，不复制底层数据。提供 `from`、`range`、`map`、`slice`、`filter`、`merge` 等与 Groovy 集合操作对等的静态方法。`protected` 构造器，静态工具类。

```java
// 空不可变 List
static <T> @Unmodifiable List<T> zl()

// from: 将数组/Iterable 包装为视图
static <T> @Unmodifiable List<T> from(int aSize, IListGetter<? extends T> aListGetter)
static <T> @Unmodifiable Collection<T> from(int aSize, Iterable<T> aIterable)
static <T> List<T> from(T[] aData)
static List<Double> from(double[] aData)  // 支持 set
static List<Integer> from(int[] aData)    // 支持 set
static List<Boolean> from(boolean[] aData)// 支持 set

// range: Python-style 整数范围（视图）
static @Unmodifiable List<Integer> range(int aStart, int aStop, int aStep)
static @Unmodifiable List<Integer> range(int aStart, int aStop)
static @Unmodifiable List<Integer> range(int aSize)

// map: 泛型/基本类型映射（视图）
static <R,T> @Unmodifiable Iterable<R> map(Iterable<T>, IUnaryFullOperator<R,? super T>)
static <R,T> @Unmodifiable List<R> map(T[], IUnaryFullOperator<R,? super T>)
static <R> @Unmodifiable List<R> map(double[], IUnaryFullOperator<R, Double>)
static <R> @Unmodifiable List<R> map(IVector, IUnaryFullOperator<R, Double>)
static <R> @Unmodifiable List<R> map(IIntVector, IUnaryFullOperator<R, Integer>)

// slice: 索引切片（视图），支持 ISlice/List<Integer>/int[]/IIndexFilter
static <T> List<T> slice(List<T>, ISlice / List<Integer> / int[] / IIndexFilter)

// filter: 惰性过滤（视图）
static <T> @Unmodifiable Iterable<T> filter(Iterable<? extends T>, IFilter<? super T>)
static @Unmodifiable IHasIntIterator filterInt(IHasIntIterator, IIndexFilter)
static @Unmodifiable IHasDoubleIterator filterDouble(IHasDoubleIterator, IDoubleFilter)

// merge: 数组/List/Iterable 合并（视图，18 个重载）
static <T> @Unmodifiable List<T> merge(T[] aBefore, T[] aAfter)
static <T> @Unmodifiable Iterable<T> merge(Iterable<? extends Iterable<? extends T>> aNestIterable)
```
