# MqOutbox

> Outbox 编排入口：事务内落库 + 事务提交后立即投递（immediate dispatch）+ relay 兜底。语义为 at-least-once，消费端需配合 MqIdempotentStore 幂等

- **包**: io.soil.jsf.mq.core.outbox

## 业务用法

```java
@Transactional
public void createOrder(OrderCmd cmd) {
    orderRepo.save(order);
    mqOutbox.save("order-topic", "created", new OrderCreatedEvent(order.getId()));
    // 事务提交后自动立即投递；失败由 MqOutboxRelay 兜底
}
```

## 方法

### save

`MqOutboxMessage save(String topic, String tag, Object payload)`

> 在业务事务内落库 Outbox（PENDING），事务提交后自动立即投递

**参数**:
- `topic` (String) — 目标 topic
- `tag` (String) — 消息 tag（可空）
- `payload` (Object) — 业务消息体（序列化为 JSON 存储）

**返回**: MqOutboxMessage — 已落库消息（id 已回填）

### dispatch

`boolean dispatch(MqOutboxMessage msg)`

> 投递单条消息：原子认领 → 发送 → 标记结果。供立即投递与 relay 兜底共用

**返回**: true=发送成功；false=认领失败或发送失败（已按退避/终态落库）

### backoffMillis

`long backoffMillis(int attempt)`

> 指数退避：initialBackoff * 2^(attempt-1)，上限 maxBackoffSeconds（public 便于测试）
