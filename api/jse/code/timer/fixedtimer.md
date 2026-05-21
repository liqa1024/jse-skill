# FixedTimer

> `jse.code.timer.FixedTimer`

**核心职能**：从构造/重置时刻开始的单过程计时器。`new FixedTimer()`。

```java
FixedTimer()
long getNanos()    // 构造时的 System.nanoTime (不稳定)
long getMillis()   // 构造时的 System.currentTimeMillis (不稳定)
double get()       // 构造到调用时刻的秒数
void reset()       // 重置起始时刻
```
