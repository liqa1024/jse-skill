# IAtomData

> `jse.atom.IAtomData`

**核心职能**：`extends IHasSymbol`。原子数据容器的只读视图——聚合了原子列表、模拟盒、种类/符号/质量信息、多种格式导出和 ASE 转换。

```java
// === 抽象方法（子类必须实现） ===
List<? extends IAtom> atoms()             // 内部原子引用列表
IAtom atom(int aIdx)                      // 指定索引的原子引用
int natoms()                               // 原子总数
int ntypes()                               // 原子种类总数（覆写 IHasSymbol）
int ntypesBond()                           // 键种类总数（无键时 0）
IBox box()                                 // 模拟盒
// 属性标志
boolean hasID()                            // 是否有 id
boolean hasBond()                          // 是否有键
boolean hasBondID()                        // 键是否有 id
boolean hasVelocity()                      // 是否有速度
boolean hasSymbol()                        // 是否有元素符号（覆写 IHasSymbol）
boolean hasMass()                          // 是否有质量
// 符号与质量
@Nullable String symbol(int aType)         // 指定种类的符号（覆写 IHasSymbol）
double mass(int aType)                     // 指定种类的质量
@Nullable IVector masses()                 // 质量向量（null if !hasMass）
// 拷贝与运算器
ISettableAtomData copy()                   // 返回可修改的深拷贝
IAtomDataOperation operation()             // 获取运算器对象

// === numpy 导出 ===
NDArray<double[]> numpy()                  // 8 列: x,y,z,id,type,vx,vy,vz
NDArray<double[]> numpyXYZ()               // 3 列: x,y,z
NDArray<double[]> numpyXYZID()             // 4 列: x,y,z,id
NDArray<double[]> numpySTD()               // 5 列: id,type,x,y,z
NDArray<double[]> numpyAll()               // 8 列: id,type,x,y,z,vx,vy,vz
NDArray<double[]> numpyVelocities()        // 3 列: vx,vy,vz

// === double[][] 导出 ===
double[][] data()                          // 每行 [x,y,z,id,type,vx,vy,vz]
double[][] dataXYZ/dataXYZID/dataSTD/dataAll/dataVelocities()

// === 便捷属性（default） ===
@Deprecated List<? extends IAtom> asList() // → atoms()
double volume()                            // box().volume()
boolean isPrism()                          // box().isPrism()
boolean isLmpStyle()                       // box().isLmpStyle()
@VisibleForTesting IAtomDataOperation op() // operation() 别名

// === ASE 转换 ===
PyObject ase()                             // 转为 ASE Atoms 对象
PyObject ase(String... symbols)            // 指定符号顺序
PyObject ase(Collection symbols)
```
