# AbstractMqConsumer

> 抽象消息消费者基类：子类声明 @RocketMQMessageListener 并实现 handleMessage 返回三态结果，基类负责 ack / broker 重试 / 失败落库与幂等编排

- **包**: io.soil.jsf.mq.core
- **实现**: `RocketMQListener<T>`

## 用法

```java
@Component
@RocketMQMessageListener(topic = "order-topic", consumerGroup = "order-group")
public class OrderConsumer extends AbstractMqConsumer<OrderCreatedEvent> {

    @Autowired
    private OrderService orderService;

    @Override
    protected ConsumeStatus handleMessage(OrderCreatedEvent msg) throws Exception {
        orderService.process(msg);
        return ConsumeStatus.SUCCESS;
    }

    // 可选：启用幂等（需容器存在 MqIdempotentStore 实现）
    @Override
    protected String idempotentKey(OrderCreatedEvent msg) {
        return msg.getOrderId();
    }
}
```

## 三态结果

| 返回值 | 基类行为 | 适用场景 |
|--------|----------|----------|
| `SUCCESS`（或 null） | ack 确认；幂等 markProcessed | 正常 |
| `RETRY_LATER` | 抛 MqConsumerException 触发 broker 重试（16 次后进 %DLQ%+group）；幂等 release | 瞬时故障 |
| `DISCARD` | 不重试；MqConsumeFailureHandler 落库；幂等 release | 不可重试失败 |

处理逻辑抛出的异常默认按 `RETRY_LATER` 处理。

## 模板方法

### handleMessage

`protected abstract ConsumeStatus handleMessage(T message) throws Exception`

> 业务处理，返回消费结果三态（返回 null 视为 SUCCESS）

### idempotentKey

`protected String idempotentKey(T message)`

> 幂等键（默认 null 不启用）。返回非空值且容器存在 MqIdempotentStore 时自动启用幂等去重

### idempotentTtlSeconds

`protected long idempotentTtlSeconds()`

> 幂等声明有效期（秒），默认 300

> 业务可直接 `mqProducer.send(...)` 纯直发，与 `mqOutbox.save(...)` 可靠发送并存互不干扰。
