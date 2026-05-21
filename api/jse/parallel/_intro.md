# `jse.parallel`

> 并行计算——统一线程池抽象（IThreadPool/IExecutorEX）、parfor/parwhile 实验性并行线程池、JNI-based MPI 包装器（完整的集合通信与点对点通信，支持 C 风格 Native API 与 Java 风格 Comm 接口）。

## 架构总览 (Architecture)

```
IThreadPool (extends AutoCloseable)
  → IExecutorEX
    ← ExecutorsEX (工厂类, 含 SERIAL_EXECUTOR)

CompletedFuture<T> (final, implements Future<T>)         — 已完成 Future 包装
MergedFuture<T, F> (implements Future<List<T>>)           — 多 Future 合并
ParforThreadPool (final, implements IThreadPool, @Experimental) — parfor/parwhile 线程池
MPIException (final, extends Exception)                   — MPI 错误异常

MPI (package-private 构造)
  ├── InitHelper (static final)                           — 静态初始化哨兵
  ├── Conf (static final)                                 — 构建配置
  ├── Group (static, implements AutoCloseable)            — MPI 进程组
  ├── Comm (static, implements AutoCloseable)             — MPI 通信器 (核心)
  ├── Op (enum)                                           — 归约操作
  ├── Datatype (enum)                                     — MPI 数据类型
  ├── Thread / Rank / Tag (static final)                  — 常量定义
  └── Native (static)                                     — C 风格原生 MPI 接口
```
