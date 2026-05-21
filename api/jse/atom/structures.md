# Structures

> `jse.atom.Structures`

**核心职能**：生成 FCC/BCC/SC/HCP 晶格结构，返回抽象引用 `IAtomData`（省内存）。纯静态方法类（`protected` 构造器）。

```java
// 面心立方
static IAtomData FCC(double cellSize, int repeatX, int repeatY, int repeatZ)
static IAtomData FCC(double cellSize, int repeat)    // 等重复

// 体心立方
static IAtomData BCC(double cellSize, int repeatX, int repeatY, int repeatZ)
static IAtomData BCC(double cellSize, int repeat)

// 简单立方
static IAtomData SC(double cellSize, int repeatX, int repeatY, int repeatZ)
static IAtomData SC(double cellSize, int repeat)

// 六方密堆积
static IAtomData HCP(double cellSize, double cellHeight, int rx, int ry, int rz)
static IAtomData HCP(double cellSize, int rx, int ry, int rz)  // 自动高度
static IAtomData HCP(double cellSize, double cellHeight, int repeat)
static IAtomData HCP(double cellSize, int repeat)

// 从已有晶胞扩胞
static IAtomData from(IAtomData lattice, int repeatX, int repeatY, int repeatZ)
static IAtomData from(IAtomData lattice, int repeat)

// @VisibleForTesting 小写别名
// :note: Groovy 脚本优先使用 fcc / bcc / sc / hcp 小写别名
@VisibleForTesting static IAtomData fcc/bcc/sc/hcp(...)
```
