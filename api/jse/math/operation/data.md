# DATA

> `jse.math.operation.DATA`

**核心职能**：与 `ARRAY` 方法命名完全镜像，但操作对象从原始数组换为免装箱迭代器接口（`IHasDoubleIterator`/`IHasIntIterator`/`IHasBooleanIterator` 等）。作为向量/矩阵运算的通用实现层。`private` 构造器，静态工具类。

```java
// === 命名模式同 ARRAY，参数从 (array, shift, len) 换为 (IHasXxxIterator) ===

// === boolean 逻辑 ===
static void ebeAnd/Or/Xor2Dest(IHasBooleanIterator lhs, IHasBooleanIterator rhs, IHasBooleanSetOnlyIterator rDest)
static void mapAnd/Or/Xor2Dest(IHasBooleanIterator lhs, boolean rhs, IHasBooleanSetOnlyIterator rDest)
static void ebeAnd/Or/Xor2This/mapAnd/Or/Xor2This/not2Dest/not2This(...)
static boolean allOfThis/anyOfThis(IHasBooleanIterator)
static int countOfThis(IHasBooleanIterator)
static void cumall/cumany/cumcount2Dest(...)

// === double 比较（产生 boolean 结果） ===
static void ebeCompare2Dest(IHasDoubleIterator lhs, IHasDoubleIterator rhs, IHasBooleanSetOnlyIterator rDest, IComparator)
static void ebeEqual/Greater/GreaterOrEqual/Less/LessOrEqual2Dest(...)
static void mapCheck2Dest(IHasDoubleIterator, IHasBooleanSetOnlyIterator, IChecker)
static void mapEqual/Greater/GreaterOrEqual/Less/LessOrEqual2Dest(...)

// === double 算术/归约/累积 ===
static void ebePlus/Minus/Multiply/Div/Mod2Dest/2This(IHasDoubleIterator, IHasDoubleIterator, IHasDoubleSetOnlyIterator)
static void mapPlus/Minus/LMinus/Multiply/Div/LDiv/Mod/LMod2Dest/2This(...)
static void mapAbs/Negative2Dest/2This(...)
static double sumOfThis/meanOfThis/prodOfThis/maxOfThis/minOfThis(IHasDoubleIterator)
static double statOfThis(IHasDoubleIterator, DoubleBinaryOperator)
static void cumsum/cummean/cumprod/cummax/cummin/cumstat2Dest(...)
static void sort/biSort(IVector/IIntVector/ILongVector, ...)

// === int 算术（同模式，使用 IHasIntIterator/IntBinaryOperator） ===
static void ebePlus/Minus/Multiply/Div/Mod2Dest/2This(...)
static void mapPlus/Minus/LMinus/Multiply/Div/LDiv/Mod/LMod2Dest/2This(...)
static void mapAbs/Negative2Dest/2This(...)
static int/exsum/sumOfThis/maxOfThis/minOfThis(IHasIntIterator)

// === complex 算术（IHasComplexDoubleIterator，实虚部分离遍历） ===
static void ebePlus/Minus/Multiply/Div2Dest/2This(IHasComplexDoubleIterator, IHasDoubleIterator, IHasComplexDoubleSetOnlyIterator)
static void ebePlus/Minus/Multiply/Div2Dest/2This(IHasComplexDoubleIterator, IHasComplexDoubleIterator, IHasComplexDoubleSetOnlyIterator)
static void mapPlus/Minus/LMinus/Multiply/Div/LDiv2Dest/2This(IHasComplexDoubleIterator, double/IComplexDouble, ...)
static void mapFill2This/ebeFill2This/vecFill2This/assign2This/forEachOfThis(...)
static void reverse2Dest/2This/sort(...)
static ComplexDouble sumOfThis/meanOfThis/prodOfThis(IHasComplexDoubleIterator)
static void cumsum/cummean/cumprod/cumstat2Dest(...)
// Groovy Closure 重载: vecFill2This/assign2This/forEachOfThis(IHasComplexDoubleIterator, Closure)

// === fill / forEach / assign (各类型通用) ===
static void mapFill2This(IHasDoubleSetOnlyIterator, double)  // 填充标量
static void ebeFill2This(IHasDoubleSetOnlyIterator, IHasDoubleIterator)  // 从迭代器填充
static void vecFill2This(IHasDoubleSetOnlyIterator, IVectorGetter)  // 从向量按索引填充
static void assign2This(IHasDoubleSetOnlyIterator, DoubleSupplier)  // 从 Supplier 分配
static void forEachOfThis(IHasDoubleIterator, DoubleConsumer)  // 逐元素遍历
// float/boolean/int/long 同理

// === 高级复合运算 ===
static void mapMultiplyThenEbePlus2This(...)  // rThis += aRHS * aMul（避免中间对象创建）
```
