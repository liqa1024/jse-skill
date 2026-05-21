# Vector

> `jse.math.vector.Vector`

**核心职能**：`extends DoubleArrayVector`。double 类型向量的 final 具体实现，支持 `mShift` 零拷贝切片（`subVec`）。提供 `builder()` 进行构造期动态追加，Builder 详见 [vector_builder.md](vector_builder.md)。

```java
// === 静态工厂 ===
static Vector zeros(int aSize)
static Vector ones(int aSize)
static Builder builder()
static Builder builder(int aInitSize)

// === 构造 ===
Vector(double[] aData)
Vector(int aSize, double[] aData)
Vector(int aSize, int aShift, double[] aData)

// === 切片 ===
Vector subVec(int aFromIdx, int aToIdx)
Vector copy()
```
