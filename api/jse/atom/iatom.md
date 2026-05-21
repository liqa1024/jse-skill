# IAtom

> `jse.atom.IAtom`

**核心职能**：`extends IXYZ`。定义原子的完整只读协议（坐标 + 种类 + 可选 id/速度/键/符号/质量）+ 多种格式导出。

```java
// === 抽象方法（覆写 IXYZ 的 x/y/z 并新增 type） ===
double x(), y(), z()            // 原子坐标（覆写 IXYZ）
int type()                      // 原子种类编号，从 1 开始
ISettableAtom copy()            // 返回可设置的深拷贝（协变返回类型）

// === 原子属性（default，默认无） ===
int id()                        // 原子 id，默认 -1
boolean hasID()                 // 是否包含真实 id，默认 false
double vx(), vy(), vz()         // 速度分量，默认 0.0
IXYZ vxyz()                     // 速度向量 new XYZ(vx,vy,vz)
boolean hasVelocity()           // 是否包含速度，默认 false
@Deprecated boolean hasVelocities()  // → hasVelocity()
@Nullable List<? extends IBond> bonds()  // 键列表，默认 null
boolean hasBond()               // 是否包含键，默认 false
int index()                     // 在 IAtomData 中的索引，默认 -1
boolean hasIndex()              // 是否包含索引信息
@Nullable String symbol()       // 元素符号，默认 null
boolean hasSymbol()             // 是否包含元素符号，默认 false
double mass()                   // 原子质量，默认 Double.NaN
boolean hasMass()               // 是否包含质量，默认 false

// === 多种导出格式 ===
NDArray<double[]> numpy()       // [x,y,z,id,type,vx,vy,vz] 8 列
NDArray<double[]> numpyXYZ()    // [x,y,z]
NDArray<double[]> numpyXYZID()  // [x,y,z,id]
NDArray<double[]> numpySTD()    // [id,type,x,y,z]
NDArray<double[]> numpyAll()    // [id,type,x,y,z,vx,vy,vz]
NDArray<double[]> numpyVelocities() // [vx,vy,vz]
double[] data()                 // 8 列 double[]
double[] dataXYZ/dataXYZID/dataSTD/dataAll/dataVelocities()
```
