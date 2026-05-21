# AbstractSettableAtomData

> `jse.atom.AbstractSettableAtomData`

**核心职能**：`abstract class extends AbstractAtomData implements ISettableAtomData`。可设置原子数据的抽象基类，覆写 `atom(int)` 为可设置版本并新增 setBox 族（正交/三斜/lammps 格式）、setAtom、setNtypes、setSymbols、setMasses 等写入操作。

```java
// === 抽象方法（覆写返回 ISettableAtom） ===
abstract ISettableAtom atom(int aIdx)

// === 种类与符号设置（默认 throw UnsupportedOperationException） ===
AbstractSettableAtomData setNtypes(int)
AbstractSettableAtomData setNoVelocity() / setHasVelocity()
AbstractSettableAtomData setSymbolOrder(String... / Collection)
AbstractSettableAtomData setSymbols(String... / Collection)
AbstractSettableAtomData setNoSymbol()
AbstractSettableAtomData setMasses(double... / Collection / IVector)
AbstractSettableAtomData setNoMass()

// === setBox 族（第一个 boolean 控制是否 validAtomPosition） ===
AbstractSettableAtomData setBox(boolean, double, double, double)
AbstractSettableAtomData setBox(boolean, IXYZ, IXYZ, IXYZ)
AbstractSettableAtomData setBox(boolean, double, double, double, double, double, double)
AbstractSettableAtomData setBox(boolean, double×9)
AbstractSettableAtomData setBox(boolean, IBox)
AbstractSettableAtomData setBoxNormal(boolean)
AbstractSettableAtomData setBoxPrism()
AbstractSettableAtomData setBoxPrism(boolean, double, double, double)
AbstractSettableAtomData setBoxPrism(boolean, double×6)
AbstractSettableAtomData setBoxXYZ(boolean, double, double, double)
AbstractSettableAtomData setBoxScale(boolean, double)

// === 内部 setter 钩子（protected，默认 throw UnsupportedOperationException） ===
protected void setBox_(double, double, double)
protected void setBox_(double, double, double, double, double, double)
protected void setBox_(double×9)
protected void scaleAtomPosition_(boolean, double)
protected void validAtomPosition_(boolean, IBox oldBox)

// === 原子修改 ===
void setAtom(int aIdx, IAtom aAtom)
List<? extends ISettableAtom> atoms()       // AbstractRandomAccessList（可 set）
@Deprecated List<? extends ISettableAtom> asList()  // → atoms()

// === 运算器（协变返回） ===
ISettableAtomDataOperation operation()
@VisibleForTesting ISettableAtomDataOperation op()

// === 内部可设置原子抽象（protected inner class） ===
protected abstract class AbstractSettableAtom_ extends AbstractSettableAtom {
    boolean hasID() / hasBond() / hasVelocity()
    @Nullable String symbol()
    boolean hasSymbol()
    double mass() / hasMass()
    int id()                       // 无 id 或 id<=0 时返回 index()+1
    int type()                     // min(type_(), ntypes())
    double vx() / vy() / vz()      // 无速度时返回 0.0
    ISettableAtom setX(double) / setY(double) / setZ(double)
    ISettableAtom setID(int)       // 检查 hasID
    ISettableAtom setType(int)     // 自动调整 setNtypes
    ISettableAtom setVx(double) / setVy(double) / setVz(double)  // 检查 hasVelocity
    protected int id_()                      // 默认 -1
    protected abstract int type_()
    protected double vx_() / vy_() / vz_()   // 默认 0.0
    protected abstract void setX_(double) / setY_(double) / setZ_(double)
    protected void setID_(int)               // throw RuntimeException
    protected abstract void setType_(int)
    protected void setVx_(double) / setVy_(double) / setVz_(double)  // throw RuntimeException
    abstract int index()
    boolean hasIndex()                       // 永远 true
}
```
