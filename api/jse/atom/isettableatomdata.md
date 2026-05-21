# ISettableAtomData

> `jse.atom.ISettableAtomData`

**核心职能**：`extends IAtomData`。增加原子/盒/种类/符号/质量的完整写入能力。setBox 族提供 12 个重载覆盖正交/三斜/lammps 格式。

```java
// === 覆写返回类型为可设置版本 ===
List<? extends ISettableAtom> atoms()             // 可设置原子列表
ISettableAtom atom(int aIdx)                      // 可设置的原子引用
ISettableAtomDataOperation operation()             // 可设置运算器（协变返回）

// === 原子修改 ===
void setAtom(int aIdx, IAtom aAtom)               // 直接覆写指定原子

// === 种类与符号设置（返回 this 链式） ===
ISettableAtomData setNtypes(int)
ISettableAtomData setSymbolOrder(String... / Collection)  // 设置符号顺序
ISettableAtomData setSymbols(String... / Collection)      // 设置符号映射
ISettableAtomData setNoSymbol()                            // 清除符号信息

// === 速度开关 ===
ISettableAtomData setNoVelocity()
ISettableAtomData setHasVelocity()

// === 质量设置 ===
ISettableAtomData setMasses(double... / Collection / IVector)
ISettableAtomData setNoMass()

// === setBox 族（第一个 boolean 控制是否 validAtomPosition） ===
ISettableAtomData setBox(boolean, double, double, double)  // 正交盒
ISettableAtomData setBox(boolean, IXYZ, IXYZ, IXYZ)        // 三斜（基向量）
ISettableAtomData setBox(boolean, double,double,double, double,double,double) // lammps 三斜 (XY,XZ,YZ)
ISettableAtomData setBox(boolean, double×9)                // 通用 9 分量
ISettableAtomData setBox(boolean, IBox)                    // 从已有 IBox 拷贝
ISettableAtomData setBoxNormal(boolean)                     // 强制正交
ISettableAtomData setBoxPrism()                             // 强制三斜（不改变原子位置）
ISettableAtomData setBoxPrism(boolean, double,double,double)          // 三斜 + 倾斜因子
ISettableAtomData setBoxPrism(boolean, double×6)                     // 三斜完整 6 参数
ISettableAtomData setBoxXYZ(boolean, double,double,double)           // 仅修改 xyz 长度
ISettableAtomData setBoxScale(boolean, double)                       // 等比缩放 + scaleAtomPosition

// 无 boolean 参数重载（默认 validAtomPosition=false）
ISettableAtomData setBox(double,double,double)
ISettableAtomData setBox(IXYZ,IXYZ,IXYZ)
ISettableAtomData setBox(...)  // 上述 12 个重载的快捷版

// === Groovy 兼容 (@VisibleForTesting) ===
@VisibleForTesting ISettableAtomDataOperation op()   // operation() 别名
@VisibleForTesting int getNtypes()
@VisibleForTesting IBox getBox()
@VisibleForTesting @Nullable List<String> getSymbols()
@VisibleForTesting @Nullable IVector getMasses()
```
