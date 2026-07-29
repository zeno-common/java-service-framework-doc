# MqIdempotentStore

> 消费幂等存储接口（依赖倒置：核心只定义协议，落库由实现模块提供，如 jsf-mq-mongodb）。协议为 claim / markProcessed / release 三段式

- **包**: io.soil.jsf.mq.core.idempotent

## 协议

- `tryClaim(key, ttl)` 原子声明处理权，false=重复投递应跳过
- `markProcessed(key)` 处理成功标记完成（终态，后续重复直接跳过）
- `release(key)` 处理失败释放声明，允许 broker 重试再次进入

## 方法

### tryClaim

`boolean tryClaim(String key, long ttlSeconds)`

> 原子声明消息处理权。返回 true=首次声明可处理；false=已被声明或已处理完成，应跳过

### markProcessed

`void markProcessed(String key)`

> 处理成功后标记完成（终态）

### release

`void release(String key)`

> 处理失败时释放声明，允许后续重试再次进入
