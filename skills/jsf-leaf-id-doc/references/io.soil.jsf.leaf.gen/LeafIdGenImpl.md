# LeafIdGenImpl

> Snowflake ID 生成器核心实现，1+42+5+8+8 bit 结构，线程安全

- **包**: io.soil.jsf.leaf.gen
- **实现接口**: `IDGen`

## 说明

`LeafIdGenImpl` 是 Snowflake 算法的核心实现，ID 结构为：1 bit 符号位 + 42 bit 时间戳 + 5 bit 数据中心ID + 8 bit 工作节点ID + 8 bit 毫秒内序号。EPOCH 起始时间为 2026-01-01 00:00:00 UTC，单节点 QPS 约 25.6 万/秒。

内置时钟回拨检测与补偿机制：回拨 ≤ 5ms 时等待 2 倍偏移时间后重试；回拨 > 5ms 直接抛出 `LeafIdException`。

## 构造

### LeafIdGenImpl

`LeafIdGenImpl(int dataCenterId, int workerId)`

> 构造 Snowflake ID 生成器

**参数**:
- `dataCenterId` (`int`) — 数据中心 ID，范围 0 ~ 31（5 bit）
- `workerId` (`int`) — 工作节点 ID，范围 0 ~ 255（8 bit）

**异常**: `LeafIdException` — dataCenterId 或 workerId 超出合法范围

## 方法

### nextId

`synchronized long nextId()`

> 生成下一个全局唯一 ID（线程安全）

**返回**: `long` — 64 位全局唯一 ID

**异常**: `LeafIdException` — 时钟回拨超过容忍阈值或等待被中断

### tilNextMillis

`protected long tilNextMillis()`

> 自旋等待直到下一毫秒，当同一毫秒内序号耗尽时调用

**返回**: `long` — 下一毫秒的时间戳

### timeGen

`protected long timeGen()`

> 获取当前时间戳（毫秒），独立方法便于测试时 Mock 时间

**返回**: `long` — 当前时间的毫秒时间戳

## 常量

| 常量 | 值 | 说明 |
|------|------|------|
| `EPOCH` | 2026-01-01 00:00:00 UTC 毫秒值 | 时间戳起始纪元 |
| `MAXIMUM_DATA_CENTER` | 31 | 数据中心 ID 最大值（5 bit） |
| `MAXIMUM_WORKER` | 255 | 工作节点 ID 最大值（8 bit） |
| `SEQUENCE_MASK` | 255 | 序号掩码（8 bit） |

## 示例

```java
// 通常不直接使用，由 LeafId 门面类间接调用
IDGen gen = new LeafIdGenImpl(0, 1);
long id = gen.nextId();
```