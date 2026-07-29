# MqOutboxStatus

> Outbox 状态枚举

- **包**: io.soil.jsf.mq.core.outbox
- **类型**: 枚举

## 枚举值

| 值 | 说明 |
|----|------|
| `PENDING` | 待投递（含退避等待） |
| `SENDING` | 已认领、发送中（锁过期视为僵尸行） |
| `SENT` | 已发送（终态） |
| `FAILED` | 重试耗尽，人工介入（终态） |
