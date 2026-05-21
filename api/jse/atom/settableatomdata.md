# SettableAtomData

> `jse.atom.SettableAtomData`

**核心职能**：`extends AbstractSettableAtomData`，`final`。`atom(idx)` 返回可设置的匿名 `ISettableAtom` 包装，写入回写内部 list，支持 setNtypes/setBox/setSymbols 等原地修改。构造器与 `AtomData` 对称但接受 `List<? extends ISettableAtom>`。

```java
// 工厂
static AtomDataBuilder<SettableAtomData> builder()

// 核心方法（覆写，返回 SettableAtomData 链式）
ISettableAtom atom(int)            // 可设置原子包装
SettableAtomData setNtypes(int)    // 可截断或扩容种类数
SettableAtomData setNoVelocity()   // 清除速度标记
SettableAtomData setNoSymbol()     // 清除符号信息
SettableAtomData setSymbols(String...)
// 继承 AbstractSettableAtomData: setBox/setBoxNormal/setBoxPrism... 全部 12 重载
```
