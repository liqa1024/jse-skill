# IPlotter

> `jse.plot.IPlotter`

**核心职能**：类似 matplotlib 的绘图接口。提供 `plot`/`loglog`/`semilogx`/`semilogy` 四种坐标模式，每种 30 个重载覆盖 `double[]`/`IVector`/`IFunc1`/`IFunc1Subs`/`Iterable<? extends Number>`/`Collection<? extends Number>` 参数（可选 `String aName`）。所有配置方法返回 `IPlotter` 自身支持链式调用。

**plot 方法族**（30 重载）：
- Y 参数类型: `double[]` | `IVector` | `IFunc1` | `Collection<? extends Number>`
- X 参数类型: `double[]` | `IVector` | `Iterable<? extends Number>`
- Y 为 `IFunc1` 时 X 可为 `IFunc1Subs`；Y 为 `double[]` 时 X 可为 `Iterable<? extends Number>`
- 每种组合有无 `@Nullable String aName` 两个变体

```java
// === 核心 plot — 每种"形状"至少列 2 条完整签名，其余同理 ===
// 单参数: Y only
ILine plot(double[] aY)
ILine plot(IVector aY)
ILine plot(IFunc1 aY)
ILine plot(Collection<? extends Number> aY)

// 双参数: X + Y (16 种类型组合)
ILine plot(double[] aX, double[] aY)
ILine plot(IVector aX, double[] aY)
ILine plot(Iterable<? extends Number> aX, double[] aY)
ILine plot(double[] aX, IVector aY)
ILine plot(IVector aX, IVector aY)
ILine plot(Iterable<? extends Number> aX, IVector aY)
ILine plot(double[] aX, IFunc1Subs aY)
ILine plot(IVector aX, IFunc1Subs aY)
ILine plot(Iterable<? extends Number> aX, IFunc1Subs aY)
ILine plot(double[] aX, Iterable<? extends Number> aY)
ILine plot(IVector aX, Iterable<? extends Number> aY)
ILine plot(Iterable<? extends Number> aX, Iterable<? extends Number> aY)

// 双参数: Y + Name (4 种 Y 类型)
ILine plot(double[] aY, @Nullable String aName)
ILine plot(IVector aY, @Nullable String aName)
ILine plot(IFunc1 aY, @Nullable String aName)
ILine plot(Collection<? extends Number> aY, @Nullable String aName)

// 三参数: X + Y + Name (12 种类型组合)
ILine plot(double[] aX, double[] aY, @Nullable String aName)
ILine plot(IVector aX, double[] aY, @Nullable String aName)
ILine plot(Iterable<? extends Number> aX, double[] aY, @Nullable String aName)
ILine plot(double[] aX, IVector aY, @Nullable String aName)
ILine plot(IVector aX, IVector aY, @Nullable String aName)
ILine plot(Iterable<? extends Number> aX, IVector aY, @Nullable String aName)
ILine plot(double[] aX, IFunc1Subs aY, @Nullable String aName)
ILine plot(IVector aX, IFunc1Subs aY, @Nullable String aName)
ILine plot(Iterable<? extends Number> aX, IFunc1Subs aY, @Nullable String aName)
ILine plot(double[] aX, Iterable<? extends Number> aY, @Nullable String aName)
ILine plot(IVector aX, Iterable<? extends Number> aY, @Nullable String aName)
ILine plot(Iterable<? extends Number> aX, Iterable<? extends Number> aY, @Nullable String aName)

// === loglog / semilogx / semilogy ===
// 各 30 重载，签名模式与 plot 完全一致，仅内部调用 xScaleLog()/yScaleLog() 预处理
ILine loglog(double[] aY)
ILine loglog(double[] aX, double[] aY)
ILine loglog(double[] aX, double[] aY, @Nullable String aName)
// ... 其余 27 种重载模式同 plot

ILine semilogx(double[] aY)
ILine semilogx(double[] aX, double[] aY)
ILine semilogx(double[] aX, double[] aY, @Nullable String aName)
// ... 其余 27 种重载模式同 plot

ILine semilogy(double[] aY)
ILine semilogy(double[] aX, double[] aY)
ILine semilogy(double[] aX, double[] aY, @Nullable String aName)
// ... 其余 27 种重载模式同 plot

// === 显示与大小 ===
static final String DEFAULT_FIGURE_NAME = "figure"
IFigure show()
IFigure show(@Nullable String aName)
IPlotter size(int aWidth, int aHeight)

// === 标题与轴标签 ===
IPlotter title(String aTitle)
IPlotter xLabel(String aXLabel)
IPlotter yLabel(String aYLabel)
IPlotter xlabel(String aXLabel)            // @VisibleForTesting 别名
IPlotter ylabel(String aYLabel)            // @VisibleForTesting 别名

// === 字体设置 ===
IPlotter fontTitle(Font aFont)
IPlotter fontLabel(Font aFont)
IPlotter fontLegend(Font aFont)
IPlotter fontTick(Font aFont)

// === 绘制范围 ===
IPlotter xRange(double aMin, double aMax)
IPlotter yRange(double aMin, double aMax)
IPlotter xrange(double aMin, double aMax)  // @VisibleForTesting 别名
IPlotter yrange(double aMin, double aMax)  // @VisibleForTesting 别名
IPlotter axis(double aMin, double aMax)    // x,y 同范围
IPlotter axis(double aXMin, double aXMax, double aYMin, double aYMax)
IPlotter axis(double[] aAxis)              // @VisibleForTesting, axis[4]

// === Tick 间隔 ===
IPlotter xTick(double aTick)
IPlotter yTick(double aTick)
IPlotter xtick(double aTick)              // @VisibleForTesting 别名
IPlotter ytick(double aTick)              // @VisibleForTesting 别名
IPlotter tick(double aTick)               // x,y 同间隔
IPlotter tick(double aXTick, double aYTick)

// === 边距 ===
IPlotter insets(double aTop, double aLeft, double aBottom, double aRight)
IPlotter insetsTop(double aTop)
IPlotter insetsLeft(double aLeft)
IPlotter insetsBottom(double aBottom)
IPlotter insetsRight(double aRight)

// === 轴类型 ===
IPlotter xScaleLog()
IPlotter yScaleLog()
IPlotter xScaleLinear()
IPlotter yScaleLinear()

// === 保存与编码 ===
void save(@Nullable String aFilePath, int aWidth, int aHeight) throws IOException
void save(@Nullable String aFilePath) throws IOException
void save() throws IOException
byte[] encode(int aWidth, int aHeight) throws IOException
byte[] encode() throws IOException

// === 数据管理 ===
IPlotter clear()
void dispose()

// === 图例与线条访问 ===
ILegend legend()
List<? extends ILine> lines()
ILine line(String aName)
ILine line(int aIdx)
int nlines()
```
