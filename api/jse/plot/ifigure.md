# IFigure

> `jse.plot.IFigure`

**核心职能**：`IPlotter.show()` 返回的图形窗口对象。管理窗口名称、大小、位置、边距，支持保存和 PNG 编码。通过 `IFigure.of(IPlotter)` 静态工厂创建简单代理。

```java
boolean isShowing()
void dispose()
IPlotter plotter()

IFigure name(String aName)
IFigure size(int aWidth, int aHeight)
IFigure location(int aX, int aY)

IFigure insets(double aTop, double aLeft, double aBottom, double aRight)
IFigure insetsTop(double aTop)
IFigure insetsLeft(double aLeft)
IFigure insetsBottom(double aBottom)
IFigure insetsRight(double aRight)

void save(@Nullable String aFilePath, int aWidth, int aHeight) throws IOException
void save(@Nullable String aFilePath) throws IOException
void save() throws IOException
byte[] encode(int aWidth, int aHeight) throws IOException
byte[] encode() throws IOException

static IFigure of(IPlotter aPlotter)
```
