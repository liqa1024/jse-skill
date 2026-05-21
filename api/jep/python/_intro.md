# `jep.python`

> Python 对象封装包。PyObject 封装 Python 对象指针，通过 JNI 提供属性访问、方法调用、类型转换等操作。jse 在此基础上扩展了 Groovy 语法集成。

## 架构总览 (Architecture)

```
JepAccess
  → PyObject — Python 对象封装，实现 AutoCloseable + GroovyObject
```

> jse 修改：PyObject 额外实现 GroovyObject，新增 `invokeMethod`/`getProperty`/`setProperty` 以及 Groovy 下标运算符 `getAt`/`putAt`（映射至 Python `__getitem__`/`__setitem__`）。
