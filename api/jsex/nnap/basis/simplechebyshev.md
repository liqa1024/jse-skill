# SimpleChebyshev

> `jsex.nnap.basis.SimpleChebyshev`

**核心职能**：`SimpleBasis` 的具体实现。纯 Java 径向基组。通过 `load` 静态工厂从 Map 反序列化，也可直接构造。

```java
// === 构造 ===
SimpleChebyshev(String[] aSymbols, int aNMax, double aRCut)
SimpleChebyshev(int aNumTypes, int aNMax, double aRCut)
static SimpleChebyshev load(String[] aSymbols, Map aMap)
static SimpleChebyshev load(int aNumTypes, Map aMap)

// === 覆写 ===
double rcut()
int size()
int ntypes()
boolean hasSymbol()
String symbol(int aType)
void forward(DoubleList aNlDx, DoubleList aNlDy, DoubleList aNlDz, IntList aNlType, DoubleArrayVector rFp, DoubleList rForwardCache, boolean aFullCache)
```
