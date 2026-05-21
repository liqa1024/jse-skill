# MPI.Datatype

> `jse.parallel.MPI.Datatype`

**核心职能**：封装 MPI 内置数据类型句柄，共 31 种。Java 侧类型（`JBYTE`/`JDOUBLE`/`JBOOLEAN`/`JCHAR`/`JSHORT`/`JINT`/`JLONG`/`JFLOAT`）直接对应 Java 基本类型内存布局；C 侧类型（`CHAR`/`SHORT`/`INT`/`LONG`/`FLOAT`/`DOUBLE`/`BYTE` 及其 `UNSIGNED_*` 变体、定宽 `INT*_T`/`UINT*_T`）对应 C 类型系统。

```java
enum Datatype {
    NULL,
    // Java 类型
    JBYTE, JDOUBLE, JBOOLEAN, JCHAR, JSHORT, JINT, JLONG, JFLOAT,
    // C 有符号类型
    CHAR, SHORT, INT, LONG, LONG_LONG, FLOAT, DOUBLE, BYTE, SIGNED_CHAR,
    // C 无符号类型
    UNSIGNED_CHAR, UNSIGNED_SHORT, UNSIGNED, UNSIGNED_LONG, UNSIGNED_LONG_LONG,
    // C 定宽类型
    INT8_T, INT16_T, INT32_T, INT64_T,
    UINT8_T, UINT16_T, UINT32_T, UINT64_T

    @ApiStatus.Internal long ptr_()
}
```
