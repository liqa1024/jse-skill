# `jse.code.iterator`

> 免装箱迭代器体系——将基本类型的迭代操作从 JDK 泛型 Iterator 中解耦，避免自动装箱/拆箱开销。

## 架构总览

```
ISetOnlyIterator<E>        →  ISetIterator<E> (extends Iterator<E> + ISetOnlyIterator<E>)

基本只读迭代器(6):  IBooleanIterator, IIntIterator, ILongIterator,
                   IFloatIterator, IDoubleIterator, IComplexDoubleIterator
基本只写迭代器(6):  I{Type}SetOnlyIterator
基本读写迭代器(6):  I{Type}SetIterator extends I{Type}Iterator + I{Type}SetOnlyIterator
拥有迭代器标记(18): IHas{Type}Iterator / IHas{Type}SetOnlyIterator / IHas{Type}SetIterator
                   (每类×6, 全部@FunctionalInterface, 提供 forEach/assign 默认方法)
```
