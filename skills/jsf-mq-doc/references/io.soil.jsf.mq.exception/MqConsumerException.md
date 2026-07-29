# MqConsumerException

> 消费者侧统一异常，继承 BaseException，错误码采用 [业务]-[编码] 规约，type() 返回 SYS

- **包**: io.soil.jsf.mq.exception
- **父类**: BaseException

## 错误码常量

| 常量 | 值 |
|------|-----|
| `MQ_CONSUME_FAILED` | MQ-CONSUME-FAILED |

## 静态工厂

### consumeFailed

`static MqConsumerException consumeFailed(Throwable cause, String msgPattern, Object... msgArgs)`

> 构造消息消费失败异常（保留原始异常链）；消费者基类在 `RETRY_LATER` 时抛出以触发 broker 重试
