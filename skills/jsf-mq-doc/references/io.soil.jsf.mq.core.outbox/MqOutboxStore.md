# MqOutboxStore

> Outbox 存储接口（依赖倒置：核心只定义协议，落库由实现模块提供，如 jsf-mq-mongodb）

- **包**: io.soil.jsf.mq.core.outbox

## 方法

### insert

`void insert(MqOutboxMessage msg)`

> 持久化 Outbox 消息，实现方须回填 `MqOutboxMessage#setId(Long)`

### fetchPending

`List<MqOutboxMessage> fetchPending(int batchSize, long now)`

> 拉取待投递行：PENDING 且 nextRetryAt<=now，或 SENDING 且 lockExpireAt<now 的僵尸行

### claim

`boolean claim(Long id, long lockExpireAt)`

> 原子认领：置 SENDING 并写入锁过期时间；返回 false 表示已被认领

### markSent

`void markSent(Long id)`

> 标记已发送（SENT）

### markFailed

`void markFailed(Long id, int attempt, long nextRetryAt)`

> 标记失败：PENDING + 退避 nextRetryAt

### markDead

`void markDead(Long id, int attempt)`

> 重试耗尽置 FAILED（终态）
