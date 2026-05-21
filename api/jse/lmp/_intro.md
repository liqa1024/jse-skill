# `jse.lmp`

> LAMMPS 集成包——LAMMPS 势函数（JNI/系统命令双模式）、原生 LAMMPS C 库封装、LmpPlugin 自定义 pair/fix、dump/thermo/log 文件读写、LAMMPS 风格模拟盒。

## 架构总览 (Architecture)

```
ILmpPotential → AbstractLmpPotential (包级可见) → LmpPotential / SystemLmpPotential
NativeLmp (JNI 封装)
LmpPlugin → Pair / Fix
```
