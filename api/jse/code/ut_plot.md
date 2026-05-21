# UT.Plot

> `jse.code.UT.Plot`

**核心职能**：`@VisibleForTesting` 静态门面——管理全局 IPlotter 列表，提供 matplotlib 风格的二维折线图绘制（plot/loglog/semilogx/semilogy 各 30 重载，覆盖数组/向量/函数/集合等多种输入），支持 IAtomData 直接投影绘图。底层接口详见 `jse.plot`。

```java
// === 绘制器 / 图形管理 ===
static IPlotter plotter()            // 创建新 IPlotter，设为当前，返回
static IPlotter plotter(int aIdx)    // 按索引取 IPlotter
static int nplotters()
static List<? extends IPlotter> plotters()

static IFigure figure()              // 创建新 IPlotter 并 show，返回 IFigure
static IFigure figure(int aIdx)      // 按索引 show
static int nfigures()
static List<? extends IFigure> figures()

static void cla()                    // 清空当前 IPlotter 数据
static void cla(boolean aAll)        // aAll=true: 清空全部 IPlotter
static void clf()                    // 销毁当前 IPlotter 并移除
static void clf(boolean aAll)        // aAll=true: 销毁全部 IPlotter

// === plot — 30 重载，同 IPlotter.plot ===
// Y only: double[] | IVector | IFunc1 | Collection<? extends Number>
static ILine plot(double[] aY)
static ILine plot(IVector aY)
static ILine plot(IFunc1 aY)
static ILine plot(Collection<? extends Number> aY)
// X + Y: 12 种类型组合
static ILine plot(double[] aX, double[] aY)
static ILine plot(IVector aX, double[] aY)
static ILine plot(Iterable<? extends Number> aX, double[] aY)
static ILine plot(double[] aX, IVector aY)
static ILine plot(IVector aX, IVector aY)
static ILine plot(Iterable<? extends Number> aX, IVector aY)
static ILine plot(double[] aX, IFunc1Subs aY)
static ILine plot(IVector aX, IFunc1Subs aY)
static ILine plot(Iterable<? extends Number> aX, IFunc1Subs aY)
static ILine plot(double[] aX, Iterable<? extends Number> aY)
static ILine plot(IVector aX, Iterable<? extends Number> aY)
static ILine plot(Iterable<? extends Number> aX, Iterable<? extends Number> aY)
// Y + Name: 4 种
static ILine plot(double[] aY, @Nullable String aName)
static ILine plot(IVector aY, @Nullable String aName)
static ILine plot(IFunc1 aY, @Nullable String aName)
static ILine plot(Collection<? extends Number> aY, @Nullable String aName)
// X + Y + Name: 12 种
static ILine plot(double[] aX, double[] aY, @Nullable String aName)
static ILine plot(IVector aX, double[] aY, @Nullable String aName)
static ILine plot(Iterable<? extends Number> aX, double[] aY, @Nullable String aName)
static ILine plot(double[] aX, IVector aY, @Nullable String aName)
static ILine plot(IVector aX, IVector aY, @Nullable String aName)
static ILine plot(Iterable<? extends Number> aX, IVector aY, @Nullable String aName)
static ILine plot(double[] aX, IFunc1Subs aY, @Nullable String aName)
static ILine plot(IVector aX, IFunc1Subs aY, @Nullable String aName)
static ILine plot(Iterable<? extends Number> aX, IFunc1Subs aY, @Nullable String aName)
static ILine plot(double[] aX, Iterable<? extends Number> aY, @Nullable String aName)
static ILine plot(IVector aX, Iterable<? extends Number> aY, @Nullable String aName)
static ILine plot(Iterable<? extends Number> aX, Iterable<? extends Number> aY, @Nullable String aName)

// === loglog / semilogx / semilogy — 各 30 重载，模式同 plot ===
static ILine loglog(double[] aY)
static ILine loglog(double[] aX, double[] aY, @Nullable String aName)
// ... 其余 28 种重载模式同 plot（先调 xScaleLog()+yScaleLog()）

static ILine semilogx(double[] aY)
static ILine semilogx(double[] aX, double[] aY, @Nullable String aName)
// ... 其余 28 种重载模式同 plot（先调 xScaleLog()）

static ILine semilogy(double[] aY)
static ILine semilogy(double[] aX, double[] aY, @Nullable String aName)
// ... 其余 28 种重载模式同 plot（先调 yScaleLog()）

// === AtomData 绘图 ===
// 绘制 IAtomData 各原子种类投影到指定轴 (x/y/z)，参数通过 Map 传入
// Map key: "Types"/"Colors"/"Sizes"/"Axis"（支持大小写别名）
static ILine[] plot(IAtomData aAtomData, Map<?, ?> aArgs)
static ILine[] plot(IAtomData aAtomData, String... aAtomTypes)
static ILine[] plot(IAtomData aAtomData)

// === 轴类型 ===
static void xScaleLog()
static void yScaleLog()
static void xScaleLinear()
static void yScaleLinear()

// === 标题 / 标签 ===
static void title(String aTitle)
static void xLabel(String aXLabel)
static void yLabel(String aYLabel)
static void xlabel(String aXLabel)       // @VisibleForTesting
static void ylabel(String aYLabel)       // @VisibleForTesting

// === 范围 ===
static void xRange(double aMin, double aMax)
static void yRange(double aMin, double aMax)
static void xrange(double aMin, double aMax)   // @VisibleForTesting
static void yrange(double aMin, double aMax)   // @VisibleForTesting
static void axis(double aMin, double aMax)
static void axis(double aXMin, double aXMax, double aYMin, double aYMax)
static void axis(double[] aAxis)

// === Tick ===
static void xTick(double aTick)
static void yTick(double aTick)
static void xtick(double aTick)          // @VisibleForTesting
static void ytick(double aTick)          // @VisibleForTesting
static void tick(double aTick)
static void tick(double aXTick, double aYTick)

// === 大小 / 保存 / 编码 ===
static void figureSize(int aWidth, int aHeight)
static void figsize(int aWidth, int aHeight)    // @VisibleForTesting 别名
static void saveFigure(@Nullable String aFilePath, int aWidth, int aHeight) throws IOException
static void saveFigure(@Nullable String aFilePath) throws IOException
static void saveFigure() throws IOException
static byte[] encodeFigure(int aWidth, int aHeight) throws IOException
static byte[] encodeFigure() throws IOException
static void savefig(@Nullable String aFilePath, int aWidth, int aHeight) throws IOException
static void savefig(@Nullable String aFilePath) throws IOException
static void savefig() throws IOException
static byte[] encodefig(int aWidth, int aHeight) throws IOException
static byte[] encodefig() throws IOException

// === 图例 / 线条访问 ===
static ILegend legend()
static List<? extends ILine> lines()
static ILine line(String aName)
static ILine line(int aIdx)
static int nlines()
```
