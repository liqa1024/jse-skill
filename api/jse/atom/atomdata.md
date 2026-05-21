# AtomData

> `jse.atom.AtomData`

**核心职能**：`extends AbstractAtomData`，`final`。内部存储 `List<IAtom>` 引用，`atom(idx)` 返回自动注入 index 的匿名包装。6 个构造器 + `static builder()`，构造器自动检测 hasID/hasVelocity/hasSymbol。

```java
// 工厂
static AtomDataBuilder<AtomData> builder()

// 构造器（逐步省略自动检测项）
AtomData(List<? extends IAtom>, int ntypes, IBox, boolean hasID, boolean hasVelocity, String... symbols)
AtomData(List<? extends IAtom>, int ntypes, IBox, boolean hasID, boolean hasVelocity)  // 自动 symbols
AtomData(List<? extends IAtom>, IBox, boolean hasID, boolean hasVelocity)               // 自动 ntypes
AtomData(List<? extends IAtom>, int ntypes, IBox)        // 自动 hasID/hasVelocity
AtomData(List<? extends IAtom>, IBox)                     // 全部自动
AtomData(List<? extends IAtom>)                           // Box = null

// 核心方法
IAtom atom(int aIdx)          // 返回带 index 的匿名 IAtom 包装
IBox box()                    // 模拟盒引用
int natoms/ntypes()
boolean hasID/hasVelocity/hasSymbol/hasMass()
String symbol(int aType)      // 元素符号
double mass(int aType)        // 原子质量 (= CS.MASS.get(symbol))
```
