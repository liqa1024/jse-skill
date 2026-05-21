# ITimer

> `jse.code.timer.ITimer`

**核心职能**：定义计时器基本操作——获取纳秒/毫秒/秒值以及重置。接口，由 `AccumulatedTimer` / `FixedTimer` 实现。标注 `@ApiStatus.Experimental`。

```java
long getNanos()
long getMillis()
double get()
void reset()
```
