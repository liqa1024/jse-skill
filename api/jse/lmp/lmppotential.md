# LmpPotential

> `jse.lmp.LmpPotential`

**核心职能**：`extends AbstractLmpPotential`。通过 JNI 调用原生 LAMMPS 库计算能量/力/维里。线程不安全（创建和访问须同一线程）。`new LmpPotential("pair_style", "pair_coeff")` / `new LmpPotential("eam/alloy", ["Ni.eam.alloy"], mpiComm)`。

```java
// === 构造器 ===
LmpPotential(String pairStyle, String[] pairCoeff, MPI.Comm)
LmpPotential(String pairStyle, String pairCoeff, MPI.Comm)
LmpPotential(String pairStyle, Collection<? extends CharSequence>, MPI.Comm)
LmpPotential(String pairStyle, String... pairCoeff)          // MPI.Comm = null

// === 生命周期 ===
boolean isClosed()
void close() throws Exception                                // 关闭势函数及内部 NativeLmp

// === 核心计算（不支持 9 分量维里） ===
void calEnergyForceVirials(IAtomData, IVector energies, IVector fX, IVector fY, IVector fZ,
    IVector vXX, IVector vYY, IVector vZZ,
    IVector vXY, IVector vXZ, IVector vYZ, ...) throws Exception

// === 初始化 ===
static class InitHelper {
    static boolean initialized()                              // JNI 库是否已初始化
    static void init()                                        // 手动触发 JNI 库初始化
}
// 继承 AbstractLmpPotential 的全部 set* 方法
```
