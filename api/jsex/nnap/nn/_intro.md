# `jsex.nnap.nn`
> NNAP 神经网络层抽象——将基组描述符映射为原子能量。提供标准前馈网络（`FeedForward`）和参数共享变体（`SharedFeedForward`）。

## 架构总览 (Architecture)

```
ISavable
  → NeuralNetwork (@Experimental @Internal)      — 神经网络抽象根类
    → FeedForward                                 — 标准前馈网络
    → SharedFeedForward                           — 参数共享前馈网络
```
