# AbstractAtomData

> `jse.atom.AbstractAtomData`

**核心职能**：`abstract class implements IAtomData`。原子数据容器的抽象基类，采用模板方法模式——子类至少实现 `atom(int)`、`box()`、`natoms()`、`ntypes()`。提供属性标志默认值、numpy/double[][] 导出、运算器和拷贝的默认实现。

```java
// === 抽象方法（子类必须实现） ===
abstract IAtom atom(int aIdx)
abstract IBox box()
abstract int natoms()
abstract int ntypes()

// === 属性标志默认实现 ===
int ntypesBond()               // 默认 0
boolean hasID()                // 默认 false
boolean hasBond()              // 默认 false
boolean hasBondID()            // 默认 false
boolean hasVelocity()          // 默认 false
boolean hasSymbol()            // 默认 false
boolean hasMass()              // 默认 false
@Nullable String symbol(int aType)   // 默认 null
double mass(int aType)         // 默认 NaN

// === 便捷访问 ===
@Nullable IVector masses()     // null 或 RefView(ntypes)

// === 原子列表引用 ===
List<? extends IAtom> atoms()  // AbstractRandomAccessList 视图

// === 运算器 ===
IAtomDataOperation operation() // AbstractAtomDataOperation 匿名实现

// === numpy 导出 ===
NDArray<double[]> numpy()            // 8 列: x,y,z,id,type,vx,vy,vz
NDArray<double[]> numpyXYZ()         // 3 列: x,y,z
NDArray<double[]> numpyXYZID()       // 4 列: x,y,z,id
NDArray<double[]> numpySTD()         // 5 列: id,type,x,y,z
NDArray<double[]> numpyAll()         // 8 列: id,type,x,y,z,vx,vy,vz
NDArray<double[]> numpyVelocities()  // 3 列: vx,vy,vz

// === double[][] 导出 ===
double[][] data()                    // 每行 [x,y,z,id,type,vx,vy,vz]
double[][] dataXYZ()
double[][] dataXYZID()
double[][] dataSTD()
double[][] dataAll()
double[][] dataVelocities()

// === 拷贝与模板方法 ===
ISettableAtomData copy()                         // List<IAtom> 深拷贝
protected ISettableAtomData newSame_()            // 同结构拷贝（operation 模板）
protected ISettableAtomData newZeros_(int, IBox)  // 全零数据（operation 模板）
protected ISettableAtomData newZeros_(int)        // → newZeros_(n, box().copy())

// === 内部原子抽象（protected inner class） ===
protected abstract class AbstractAtom_ extends AbstractAtom {
    boolean hasID()                // → outer.hasID()
    boolean hasBond()              // → outer.hasBond()
    boolean hasVelocity()          // → outer.hasVelocity()
    @Nullable String symbol()      // → outer.symbol(type())
    boolean hasSymbol()            // → outer.hasSymbol()
    double mass()                  // → outer.mass(type())
    boolean hasMass()              // → outer.hasMass()
    int id()                       // 无 id 或 id<=0 时返回 index()+1
    int type()                     // min(type_(), ntypes())
    double vx() / vy() / vz()      // 无速度时返回 0.0
    protected abstract int id_()
    protected abstract int type_()
    protected double vx_() / vy_() / vz_()  // 默认 0.0
    abstract int index()
    boolean hasIndex()             // 永远 true
}

// === 内部键抽象（protected inner class） ===
protected abstract class AbstractBond_ extends AbstractBond {
    boolean hasID()                // → outer.hasBondID()
    int type()                     // min(type_(), ntypesBond())
    IAtom bondAtom()               // → atom(bondIndex())
    protected abstract int type_()
}
```
