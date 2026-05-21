# IZeroBoundFunc2

> `jse.math.function.IZeroBoundFunc2`

**核心职能**：二维零边界标记接口，继承 `IFunc2`。标记函数在指定边界外的取值为 0，用于微分/积分/卷积运算的裁剪优化。

```java
// 零边界标记
double zeroBoundNegX()                                              // x 负向零边界位置
double zeroBoundPosX()                                              // x 正向零边界位置
double zeroBoundNegY()                                              // y 负向零边界位置
double zeroBoundPosY()                                              // y 正向零边界位置
```
