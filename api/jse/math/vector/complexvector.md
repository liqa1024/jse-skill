# ComplexVector

> `jse.math.vector.ComplexVector`

**核心职能**：`final class extends BiDoubleArrayVector`。复类型向量的 final 具体实现，使用 `double[2][]` 交错存储，支持 `mShift` 零拷贝切片（`subVec`）。提供静态工厂方法和 Builder 进行构造期动态追加，Builder 详见 [complexvector_builder.md](complexvector_builder.md)。

```java
// === 静态工厂 ===
static ComplexVector zeros(int aSize)
static ComplexVector ones(int aSize)
static Builder builder()
static Builder builder(int aInitSize)

// === 构造 ===
ComplexVector(double[][] aData)
ComplexVector(int aSize, double[][] aData)
ComplexVector(int aSize, int aShift, double[][] aData)

// === IDataShell ===
void setInternalDataSize(int aSize)
void setInternalDataShift(int aShift)

// === 元素访问 (get) ===
final int size()
final ComplexDouble get(int aIdx)
final double getReal(int aIdx)
final double getImag(int aIdx)
final boolean isEmpty()
final ComplexDouble last()
final ComplexDouble first()

// === 元素访问 (set) ===
final void set(int aIdx, IComplexDouble aValue)
final void set(int aIdx, ComplexDouble aValue)
final void set(int aIdx, double aValue)
final void set(int aIdx, double aReal, double aImag)
final void setReal(int aIdx, double aReal)
final void setImag(int aIdx, double aImag)

// === 元素访问 (getAndSet) ===
final ComplexDouble getAndSet(int aIdx, IComplexDouble aValue)
final ComplexDouble getAndSet(int aIdx, ComplexDouble aValue)
final ComplexDouble getAndSet(int aIdx, double aValue)
final ComplexDouble getAndSet(int aIdx, double aReal, double aImag)
final double getAndSetReal(int aIdx, double aReal)
final double getAndSetImag(int aIdx, double aImag)

// === 单元素原子操作 ===
final void add(int aIdx, IComplexDouble aDelta)
final void add(int aIdx, ComplexDouble aDelta)
final void add(int aIdx, double aDelta)
final void addImag(int aIdx, double aImag)
final void update(int aIdx, IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
final void updateReal(int aIdx, DoubleUnaryOperator aRealOpt)
final void updateImag(int aIdx, DoubleUnaryOperator aImagOpt)
final ComplexDouble getAndUpdate(int aIdx, IUnaryFullOperator<? extends IComplexDouble, ? super ComplexDouble> aOpt)
final double getAndUpdateReal(int aIdx, DoubleUnaryOperator aRealOpt)
final double getAndUpdateImag(int aIdx, DoubleUnaryOperator aImagOpt)

// === 交换 ===
final void swap(int aIdx1, int aIdx2)

// === 切片与拷贝 ===
final ComplexVector subVec(int aFromIdx, int aToIdx)
final ComplexVector copy()

// === 转换 ===
final Vector real()
final Vector imag()
final int internalDataShift()
final double @Nullable[][] getIfHasSameOrderData(Object aObj)

// === 迭代器 ===
final IComplexDoubleIterator iterator()
final IComplexDoubleSetIterator setIterator()
```
