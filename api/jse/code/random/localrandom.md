# LocalRandom

> `jse.code.random.LocalRandom`

**核心职能**：完全局部变量的线程安全 LCG，算法与 `java.util.Random` 一致。`new LocalRandom()` 或 `new LocalRandom(long seed)`。

```java
LocalRandom() / LocalRandom(long seed)
void setSeed(long seed)
// 实现 IRandom 所有抽象方法
```
