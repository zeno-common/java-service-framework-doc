# MqOutboxMessage

> Outbox 消息 POJO（与具体存储无关），状态/重试/锁字段齐全

- **包**: io.soil.jsf.mq.core.outbox
- **注解**: @Getter @Setter

## 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `id` | Long | 消息 ID（由存储实现生成并回填） |
| `topic` | String | 目标 topic |
| `tag` | String | 消息 tag（可空） |
| `payload` | String | 业务消息体 JSON |
| `status` | MqOutboxStatus | 状态，默认 PENDING |
| `attempt` | int | 已尝试发送次数 |
| `nextRetryAt` | long | 下次可重试时间（epoch millis），PENDING 行仅 nextRetryAt<=now 时会被 relay 捞取 |
| `lockExpireAt` | long | 认领锁过期时间（epoch millis），SENDING 行锁过期视为僵尸行 |

## 方法

### destination

`String destination()`

> 发送目的地：`topic` 或 `topic:tag`
