# IHasSymbol

> `jse.atom.IHasSymbol`

**核心职能**：定义元素种类与符号的映射关系，提供种类映射工具方法。无基底接口。

```java
// === 抽象方法 ===
int ntypes()                               // 原子种类总数
boolean hasSymbol()                        // 是否包含元素符号信息
@Nullable String symbol(int aType)         // 指定种类编号的元素符号

// === 查询与映射（default） ===
@Nullable List<@Nullable String> symbols() // 按种类排序的符号列表（惰性构建）
IntUnaryOperator typeMap(IAtomData)        // 获取与目标 AtomData 的种类编号映射
boolean sameSymbolOrder(Collection)        // 判断符号顺序是否一致
int typeOf(String aSymbol)                 // 根据符号字符串查询种类编号
void typeMapCheck(int, IntUnaryOperator)   // 验证种类映射不超过自身种类数

// === @ApiStatus.Internal: static 工具方法 ===
@ApiStatus.Internal static IntUnaryOperator typeMap_(List<String>, IAtomData)
@ApiStatus.Internal static boolean sameSymbolOrder_(List<String>, Collection)
@ApiStatus.Internal static int typeOf_(List<String>, String)
```
