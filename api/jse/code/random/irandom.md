# IRandom

> `jse.code.random.IRandom`

**核心职能**：统一随机数生成抽象，弥补低版本 JDK 缺少 `RandomGenerator` 的问题。`IRandom.of(Random)` / `IRandom.of(SplittableRandom)` / `IRandom.of(Object)` 静态工厂。

```java
// 抽象方法
void nextBytes(byte[] bytes)
int nextInt(); long nextLong(); boolean nextBoolean()
float nextFloat(); double nextDouble(); double nextGaussian()

// 带范围的 default 方法
default int nextInt(int bound) / nextInt(int origin, int bound)
default long nextLong(long bound) / nextLong(long origin, long bound)
default float nextFloat(float bound) / nextFloat(float origin, float bound)
default double nextDouble(double bound) / nextDouble(double origin, double bound)
default double nextGaussian(double mean, double stddev)
default Random asRandom()

// 静态工厂
static IRandom of(Random aRng)
static IRandom of(SplittableRandom aRng)
static IRandom of(Object aRng)
```
