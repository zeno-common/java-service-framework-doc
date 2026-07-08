# LeafId

> 静态工具门面，提供全局唯一的 `nextId()` 入口，基于 Snowflake 算法生成分布式唯一 ID

- **包**: io.soil.jsf.leaf.gen
- **父类**: 无（静态工具类）

## 说明

`LeafId` 是 Leaf ID 生成器的静态门面类，由 `LeafAutoConfig` 在 Spring 容器启动时通过 `@PostConstruct` 初始化内部 `LeafIdGenImpl` 实例。业务代码只需调用 `LeafId.nextId()` 即可获取全局唯一 ID，无需关心底层协调器类型。

## 方法

### nextId

`static long nextId()`

> 生成下一个全局唯一 ID（线程安全）

**返回**: `long` — 64 位全局唯一 ID

**异常**: `LeafIdException` — 时钟回拨超过容忍阈值或内部生成器未初始化

## 示例

```java
long id = LeafId.nextId();
```