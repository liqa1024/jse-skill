# IntDeque

> `jse.code.collection.IntDeque`

**核心职能**：循环 `int[]` 后端，支持两端高效增删 + 随机访问，提供 Queue 和 Stack 语义。`new IntDeque()` 或 `new IntDeque(int)`。

```java
// 随机访问: get/set/size/last/first, getFirst/getLast
// 双端操作: addFirst/addLast, removeFirst/removeLast
// Queue: add/remove/element
// Stack: push/pop
// 工具: trimToSize/clear/forEach(IntConsumer)/asList/asVec/copy2vec
```
