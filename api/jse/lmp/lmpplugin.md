# LmpPlugin

> `jse.lmp.LmpPlugin`

**核心职能**：支持自定义 `pair_style jse` 和 `fix jse` 的 Groovy/Java 实现，包含两个核心抽象内部类 `Pair` 和 `Fix`，通过反射从类名或 Groovy 脚本路径加载。仅从 LAMMPS 侧通过 JNI 反射实例化。

```java
// === 配置 ===
static class Conf {
    static String JVM_XMX = "1g"      // JVM 最大内存
    static String LMP_VERSION          // LAMMPS 版本，默认自动检测
    static boolean DEBUG               // Debug 模式开关
}
static class InitHelper {
    static boolean initialized()       // 插件库是否已初始化
    static void init()                 // 手动触发初始化
}

// 位掩码常量
static final int SBBITS=30, HISTBITS=29
static final int NEIGHMASK=0x1FFFFFFF, HISTMASK=0xDFFFFFFF, SPECIALMASK=0x3FFFFFFF
```
