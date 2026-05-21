# UnsafeJNI

> `jse.clib.UnsafeJNI`

**核心职能**：标记可能直接或间接调用 JNI 的方法/构造器，在参数非法、生命周期错误、线程不匹配等情况下可能导致 JVM 段错误（SIGSEGV/SIGBUS）直接崩溃。仅用于**文档和开发期提示**，不产生任何编译期或运行期行为。`@Documented @Retention(SOURCE) @Target({METHOD, CONSTRUCTOR})`。

```java
@UnsafeJNI("原因说明")                // value() 描述不安全原因或使用要求
```
