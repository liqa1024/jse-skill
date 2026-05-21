# IZeroBoundFunc1

> `jse.math.function.IZeroBoundFunc1`

**核心职能**：一维零边界标记接口，继承 `IFunc1`。标记函数在指定左右边界外的取值为 0，用于微分/积分/卷积运算的裁剪优化。

```java
// 零边界标记
double zeroBoundL()                                                 // 左侧零边界位置
double zeroBoundR()                                                 // 右侧零边界位置
```
