# `jse.math.operation`

> 逐元素向量运算的底层实现。**ARRAY** 直接操作 `double[]/int[]/boolean[]` 数组（含 shift/offset，便于编译器 SIMD 优化）；**DATA** 基于免装箱迭代器接口（`IHasDoubleIterator` 等）实现相同语义。
