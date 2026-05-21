# IDataShell

> `jse.math.IDataShell`

**核心职能**：定义数据与外壳的转换协议，支持零拷贝访问/修改底层数组。广泛用于向量/矩阵的底层优化。无基底接口。

```java
// === 抽象方法 ===
D internalData()                                       // 获取内部数据引用（子类必须实现）
int internalDataSize()                                 // 有效数据长度

// === 可覆写 ===
void setInternalData(D) / setInternalDataSize(int) / setInternalDataShift(int)  // 默认抛异常
int internalDataShift() → 0                            // 数据偏移

// === 长度校验 (@ApiStatus.Experimental) ===
@ApiStatus.Experimental D internalDataWithLengthCheck()
@ApiStatus.Experimental D internalDataWithLengthCheck(int aSize)
@ApiStatus.Experimental D internalDataWithLengthCheck(int aSize, int aShift)

// === @ApiStatus.Internal ===
@ApiStatus.Internal @Nullable D getIfHasSameOrderData(Object)

// === 静态工具 ===
static int internalDataShift/size(Object)
static <D> IDataShell<D> of(int aSize, D aData)        // 工厂方法
```

> **`SimpleDataShell<D>`**（包级可见）为内部实现，Groovy 不可直接访问。
