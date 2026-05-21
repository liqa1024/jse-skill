# VoronoiExtensions

> `jsex.voronoi.VoronoiExtensions`

**核心职能**：静态扩展方法，为 `AtomicParameterCalculator` 注入 Voronoi 分析。内部串行实现，通过镜像原子近似处理周期边界条件（`aRCutOff` 越大越准确但越慢）。返回 `ICalculator`（`List<IVertex> & RandomAccess`），支持阈值配置的链式调用。

```java
// === ICalculator 接口 ===
interface ICalculator extends List<VoronoiBuilder.IVertex>, RandomAccess {
    ICalculator setNoWarning(boolean aNoWarning)
    ICalculator setNoWarning()
    ICalculator setAreaThreshold(double aAreaThreshold)
    ICalculator setLengthThreshold(double aLengthThreshold)
    ICalculator setAreaThresholdAbs(double aAreaThresholdAbs)
    ICalculator setLengthThresholdAbs(double aLengthThresholdAbs)
    ICalculator setIndexLength(int aIndexLength)
}

// === 静态工厂 (6 个重载，参数默认值链式递减) ===
static ICalculator calVoronoi(AtomicParameterCalculator self, double aRCutOff, boolean aNoWarning, int aIndexLength, double aAreaThreshold, double aLengthThreshold)
static ICalculator calVoronoi(AtomicParameterCalculator self, double aRCutOff, boolean aNoWarning, int aIndexLength, double aAreaThreshold)
static ICalculator calVoronoi(AtomicParameterCalculator self, double aRCutOff, boolean aNoWarning, int aIndexLength)
static ICalculator calVoronoi(AtomicParameterCalculator self, double aRCutOff, boolean aNoWarning)
static ICalculator calVoronoi(AtomicParameterCalculator self, double aRCutOff)
static ICalculator calVoronoi(AtomicParameterCalculator self)  // rcut = unitLen*3
```
