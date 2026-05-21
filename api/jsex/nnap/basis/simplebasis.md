# SimpleBasis

> `jsex.nnap.basis.SimpleBasis`

> 此类标记为 `@ApiStatus.Experimental`

**核心职能**：纯 Java 实现的基组抽象（无需 JIT 编译），`implements IHasSymbol, AutoCloseable`。通过 `eval`/`evalAll` 直接计算描述符，适合原型验证和接口稳定性要求高的场景。

```java
// === 查询 ===
abstract double rcut()
abstract int size()
int ntypes()                                     // 返回 1（单元素）
boolean hasSymbol()                              // 返回 false

// === 描述符计算 ===
@ApiStatus.Internal void forward(DoubleList aNlDx, DoubleList aNlDy, DoubleList aNlDz, IntList aNlType, DoubleArrayVector rFp, DoubleList rForwardCache, boolean aFullCache)
void eval(DoubleList aNlDx, DoubleList aNlDy, DoubleList aNlDz, IntList aNlType, DoubleArrayVector rFp)
void eval(AtomicParameterCalculator aAPC, int aIdx, IntUnaryOperator aTypeMap, DoubleArrayVector rFp)
void eval(AtomicParameterCalculator aAPC, int aIdx, DoubleArrayVector rFp)
List<Vector> evalAll(IAtomData aAtomData)        // 批量计算所有原子描述符

// === 生命周期 ===
boolean isClosed()
void close()
```
