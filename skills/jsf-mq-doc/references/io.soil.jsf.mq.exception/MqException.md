# MqException

> jsf-mq 统一异常，继承 BaseException，错误码 [业务]-[编码]（如 MQ-SEND-FAILED / MQ-CONSUME-FAILED），type() 返回 SYS

- **包**: io.soil.jsf.mq.exception
- **父类**: BaseException

## 常量

| 常量 | 值 |
|------|-----|
| `MQ_SEND_FAILED` | MQ-SEND-FAILED |
| `MQ_CONSUME_FAILED` | MQ-CONSUME-FAILED |
| `MQ_PRODUCER_NOT_AVAILABLE` | MQ-PRODUCER-NOT-AVAILABLE |

## 静态工厂

### sendFailed

`static MqException sendFailed(Throwable cause, String msgPattern, Object... args)`

> 构造消息发送失败异常（保留原始异常链）

### consumeFailed

`static MqException consumeFailed(Throwable cause, String msgPattern, Object... args)`

> 构造消息消费失败异常（保留原始异常链）
