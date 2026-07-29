# MqProducer

> 统一消息生产者，封装 RocketMQTemplate 的同步/异步/单向/延迟四类发送，异常统一包装为 MqException

- **包**: io.soil.jsf.mq.core
- **父类**: 无（普通类）

## 构造

| 签名 | 说明 |
|------|------|
| `MqProducer(RocketMQTemplate rocketMQTemplate)` | 由自动配置注入，业务一般直接注入使用 |

## 方法

### send

`SendResult send(String destination, Object payload)`

> 同步发送消息

**参数**:
- `destination` (String) — topic 或 `topic:tag`
- `payload` (Object) — 消息体（自动序列化）

**返回**: SendResult — 发送结果

**异常**: `MqException` — 发送失败（保留原始异常链）

**示例**:
```java
SendResult r = mqProducer.send("order-topic", new OrderCreatedEvent(id));
```

### sendAsync

`void sendAsync(String destination, Object payload, Consumer<SendResult> onSuccess)`

> 异步发送（仅成功回调，异常包装为 MqException 抛出）

**参数**: 见 `send`；`onSuccess` — 成功回调

**异常**: `MqException` — 异步发送异常

另有重载 `sendAsync(destination, payload, onSuccess, onError)` 分离成功/失败回调（onError 入参为包装后的 `MqException`）。

### sendOneway

`void sendOneway(String destination, Object payload)`

> 单向发送（不关心结果，无返回、不保证可靠）

### sendDelay

`SendResult sendDelay(String destination, Object payload, int delayLevel)`

> 发送延迟消息（同步），delayLevel 为 RocketMQ 延迟级别 1~18

**参数**: `delayLevel` (int) — RocketMQ 延迟级别

**异常**: `MqException` — 发送失败
