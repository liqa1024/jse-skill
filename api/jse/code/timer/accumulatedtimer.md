# AccumulatedTimer

> `jse.code.timer.AccumulatedTimer`

**核心职能**：通过 `from()` / `to()` 成对调用累加多次时间片段。`new AccumulatedTimer()`。

```java
AccumulatedTimer()
void from()          // 记录开始时间点
void to()            // 停止并将本段耗时累加入总时间
long getNanos/millis/get/reset  // ITimer 实现
```
