# NNAPExtensions

> `jsex.nnap.NNAPExtensions`

**核心职能**：静态扩展方法，为 `AtomicParameterCalculator` 注入纯 Java 实现的 NNAP 基组计算。使用 `SimpleSphericalChebyshev` 提供与 JIT 版本一致的结果，保证最高兼容性。

```java
static List<Vector> calBasisNNAP(AtomicParameterCalculator self, int aNMax, int aLMax, double aRCutOff)
```
