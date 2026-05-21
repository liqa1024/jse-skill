# MPI.Group

> `jse.parallel.MPI.Group`

**核心职能**：`static class implements AutoCloseable`。封装 MPI Group 句柄（`long` 指针）。预置 `NULL`/`EMPTY` 静态实例。支持 `difference`/`excl`/`incl`/`intersection`/`union` 五种子集构造操作。`close()` 调用 `MPI_Group_free`。

```java
static final Group NULL, EMPTY

int rank() throws MPIException
int size() throws MPIException
void close() throws MPIException

// === 子集构造 ===
Group difference(Group aRHS) throws MPIException
Group excl(int aN, int[] aRanks) throws MPIException
Group excl(int[] aRanks) throws MPIException
Group incl(int aN, int[] aRanks) throws MPIException
Group incl(int[] aRanks) throws MPIException
Group intersection(Group aRHS) throws MPIException
Group union(Group aRHS) throws MPIException

// === 内部 (JNI 桥接) ===
@ApiStatus.Internal static Group of(long aPtr)
@ApiStatus.Internal long ptr_()
```
