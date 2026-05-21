# MPI.Op

> `jse.parallel.MPI.Op`

**核心职能**：封装 MPI 内置归约操作句柄。包含算术（`MAX`/`MIN`/`SUM`/`PROD`）、逻辑（`LAND`/`LOR`/`LXOR`）、位运算（`BAND`/`BOR`/`BXOR`）、带位置（`MINLOC`/`MAXLOC`）及 `REPLACE`/`NULL`。

```java
enum Op {
    NULL, MAX, MIN, SUM, PROD,
    LAND, BAND, LOR, BOR, LXOR, BXOR,
    MINLOC, MAXLOC, REPLACE

    @ApiStatus.Internal long ptr_()
}
```
