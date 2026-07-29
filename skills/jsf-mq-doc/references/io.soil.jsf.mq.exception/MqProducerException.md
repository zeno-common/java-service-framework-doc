# MqProducerException

> 生产者侧统一异常，继承 BaseException，错误码采用 [业务]-[编码] 规约，type() 返回 SYS

- **包**: io.soil.jsf.mq.exception
- **父类**: BaseException

## 错误码常量

| 常量 | 值 |
|------|-----|
| `MQ_SEND_FAILED` | MQ-SEND-FAILED |
| `MQ_PRODUCER_NOT_AVAILABLE` | MQ-PRODUCER-NOT-AVAILABLE |

## 静态工厂

### sendFailed

`static MqProducerException sendFailed(Throwable cause, String msgPattern, Object... msgArgs)`

> 构造消息发送失败异常（保留原始异常链）

### producerNotAvailable

`static MqProducerException producerNotAvailable(String msgPattern, Object... msgArgs)`

> 构造生产者不可用异常（RocketMQ 未初始化 / RocketMQTemplate 缺失）
