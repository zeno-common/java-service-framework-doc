# IDGen

> ID 生成器顶层接口，定义 nextId 方法

- **包**: io.soil.jsf.leaf
- **类型**: 接口

## 说明

`IDGen` 是 ID 生成器的顶层接口，定义了生成下一个唯一 ID 的方法。`LeafIdGenImpl` 是其核心实现。

## 方法

### nextId

`long nextId()`

> 生成下一个全局唯一 ID

**返回**: `long` — 64 位全局唯一 ID