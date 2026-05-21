# AbstractLmpPotential

> `jse.lmp.AbstractLmpPotential`

**核心职能**：`implements IPotential`。包级可见的抽象基类，封装 `pair_style/pair_coeff/units/beforeCommands/lastCommands` 公共配置。不可直接实例化，Groovy 通过子类 `LmpPotential`（JNI）或 `SystemLmpPotential`（系统命令）使用。

```java
// 公共配置（返回 this 链式，通过子类继承访问）
AbstractLmpPotential setPairStyle(String)           // 设置 pair_style
AbstractLmpPotential setPairCoeff(String...)         // 设置 pair_coeff
AbstractLmpPotential setUnits(String)                // 设置 LAMMPS 单位制，默认 "metal"
AbstractLmpPotential setBeforeCommands(String)      // LAMMPS 运行前执行的命令（换行分隔）
AbstractLmpPotential setLastCommands(String)         // LAMMPS 运行最后执行的命令（如 pair_modify）
String units()                                       // 获取当前单位制

// 不支持部分原子能量
double calEnergyAt(IAtomData, ISlice) → UnsupportedOperationException

// 单位换算常量
static final double BAR_TO_EV      // metal 单位: bar → eV/Å³
static final double ATM_TO_KCAL    // real 单位: atm → (kcal/mol)/Å³
static final double PA_TO_HARTREE  // electron 单位: Pa → Hartree/Bohr³
```
