# SimpleSphericalChebyshev

> `jsex.nnap.basis.SimpleSphericalChebyshev`

**核心职能**：`SimpleBasis` 的具体实现。纯 Java 径向+角向基组（含预计算 Wigner 3j 符号常量）。通过 `load` 静态工厂从 Map 反序列化，也可直接构造。

```java
// === 构造 ===
SimpleSphericalChebyshev(String[] aSymbols, int aNMax, int aLMax, double aRCut)
SimpleSphericalChebyshev(int aNumTypes, int aNMax, int aLMax, double aRCut)
static SimpleSphericalChebyshev load(String[] aSymbols, Map aMap)
static SimpleSphericalChebyshev load(int aNumTypes, Map aMap)

// === 预计算 Wigner 3j 符号常量 ===
static double WIGNER_222_000, WIGNER_222_011, WIGNER_222_022, WIGNER_222_112
static double WIGNER_112_000, WIGNER_112_011, WIGNER_112_110, WIGNER_112_112
// ... 更多 l=2,3,4 组合的 Wigner 符号常量（约 80+ 个）

// === 覆写 ===
double rcut()
int size()
int ntypes()
boolean hasSymbol()
String symbol(int aType)
void forward(DoubleList aNlDx, DoubleList aNlDy, DoubleList aNlDz, IntList aNlType, DoubleArrayVector rFp, DoubleList rForwardCache, boolean aFullCache)
```
