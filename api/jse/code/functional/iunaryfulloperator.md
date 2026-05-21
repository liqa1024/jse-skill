# IUnaryFullOperator

> `jse.code.functional.IUnaryFullOperator`

**核心职能**：接收一个泛型参数，返回一个泛型结果。扩展自 `java.util.function.Function<T,R>`，含静态 `identity`。是 `map`/`filter` 操作的核心回调接口。

```java
R apply(T aInput)
```
