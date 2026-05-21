# SphericalChebyshev

> `jsex.nnap.basis.SphericalChebyshev`

**核心职能**：JIT 编译的 Chebyshev 多项式基组（径向+角向）。含径向+角向（球谐函数）描述符（默认 `nmax=5, lmax=6`）。继承 `WTypeBasis`，支持化学种类编码（wtype: default/exfull/fuse 等）和后融合（post_fuse）降维。

```java
// === 静态工厂 ===
static SphericalChebyshev load(int aNumTypes, Map aMap)

// === 常量 ===
static int DEFAULT_NMAX = 5
static int DEFAULT_LMAX = 6
static int DEFAULT_L3MAX = 0
static int DEFAULT_L4MAX = 0
static double DEFAULT_RCUT = 6.0

// === WTypeBasis 提供的公开常量（通过继承访问） ===
static int WTYPE_DEFAULT = 0                     // 简单种类对
static int WTYPE_NONE = -1                       // 无种类编码
static int WTYPE_FULL = 2                        // 全种类编码
static int WTYPE_EXFULL = 3                      // 扩展全种类编码（默认）
static int WTYPE_FUSE = 4                        // 可训练融合权重
static int WTYPE_RFUSE = 5                       // 受限融合权重
static int WTYPE_EXFUSE = 6                      // 扩展可训练融合权重

// === 覆写 ===
int size()                                       // 基组输出维度
void save(Map rSaveTo)                           // 序列化（type: "spherical_chebyshev"）
int forwardCacheSize(int aNumNei)
int backwardCacheSize(int aNumNei)
int backwardBackwardCacheSize(int aNumNei)
```
