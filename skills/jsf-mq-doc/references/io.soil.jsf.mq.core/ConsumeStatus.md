# ConsumeStatus

> 消费结果三态枚举，由 AbstractMqConsumer#handleMessage 返回

- **包**: io.soil.jsf.mq.core
- **类型**: 枚举

## 枚举值

| 值 | 说明 |
|----|------|
| `SUCCESS` | 消费成功，正常 ack 确认 |
| `RETRY_LATER` | 稍后重试：抛 MqException 触发 broker 重试（指数退避，默认 16 次后进入 %DLQ%+group 死信队列），适用瞬时故障 |
| `DISCARD` | 丢弃不重试：判定不可重试失败，交 MqConsumeFailureHandler 落库供重放 |
