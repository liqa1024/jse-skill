# PyObject

> `jep.python.PyObject`

**核心职能**：封装 Python 对象指针，继承 `JepAccess`，实现 `AutoCloseable` + `GroovyObject`（jse 扩展）。通过 JNI 提供 Python 属性访问、方法调用、类型转换与动态代理。非线程安全，仅可在创建线程上使用；所属 `Interpreter` 关闭后 PyObject 即失效。

```java
// === 构造与内部指针 ===
protected PyObject(Jep jep, long pyObject)
protected long getPyObject()
protected long tstate()

// === 属性访问 ===
Object getAttr(String attr_name)
<T> T getAttr(String attr_name, Class<T> clazz)
void setAttr(String attr_name, Object o)
void delAttr(String attr_name)

// === Java 标准方法 ===
boolean equals(Object obj)
String toString()
int hashCode()

// === 类型转换与代理 ===
<T> T as(Class<T> expectedType)
<T> T proxy(Class<T> primaryInterface, Class<?>... extraInterfaces)

// === 生命周期 ===
void close()

// === jse 扩展：Groovy 方法调用集成 ===
@SuppressWarnings("unchecked")
Object invokeMethod(String name, Object args)                               // :note: jse 扩展：实现 GroovyObject，将 Groovy 方法调用自动委托至 Python 对应方法。末尾参数为 Map 时自动作为 Python kwargs 传入

Object getProperty(String propertyName)                                     // :note: jse 扩展：Groovy 属性读取，委托至 getAttr
void setProperty(String propertyName, Object newValue)                      // :note: jse 扩展：Groovy 属性写入，委托至 setAttr
MetaClass getMetaClass()                                                    // :note: jse 扩展：GroovyObject 元类支持
void setMetaClass(MetaClass metaClass)                                      // :note: jse 扩展：GroovyObject 元类支持

// === jse 扩展：Python 运算符重载 ===
Object getAt(int aIdx)                                                      // :note: jse 扩展：Groovy 下标运算符，映射至 Python __getitem__
void putAt(int aIdx, Object aValue)                                         // :note: jse 扩展：Groovy 下标运算符，映射至 Python __setitem__
```
