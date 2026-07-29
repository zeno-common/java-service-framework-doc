# MqConsumeFailureRecord

> 消费失败记录 POJO（核心，与具体存储无关），保存完整消息上下文供排查与重放

- **包**: io.soil.jsf.mq.core.failure
- **注解**: @Getter @Setter

## 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `id` | Long | 记录 ID（存储生成并回填） |
| `topic` | String | 消息 topic |
| `tag` | String | 消息 tag |
| `consumerGroup` | String | 消费者组 |
| `consumerClass` | String | 消费者类全名 |
| `messageId` | String | 消息 ID（如有） |
| `bizKey` | String | 业务键/幂等键（如有） |
| `payload` | String | 消息体 JSON |
| `errorMsg` | String | 异常摘要 |
| `stackTrace` | String | 异常堆栈 |
| `status` | MqConsumeFailureStatus | 状态，默认 PENDING |
| `failedAt` | OffsetDateTime | 失败时间 |
| `replayedAt` | OffsetDateTime | 重放时间 |
