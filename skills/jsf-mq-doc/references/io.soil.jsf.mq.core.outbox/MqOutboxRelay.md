# MqOutboxRelay

> Outbox 兜底补发器：定时扫描待投递行（PENDING 到期 + SENDING 锁过期僵尸行），逐条走 MqOutbox#dispatch，集群多实例并发安全

- **包**: io.soil.jsf.mq.core.outbox

## 启用

依赖应用开启 `@EnableScheduling`；扫描间隔由 `jsf.mq.producer.outbox.relay.interval` 控制（默认 5000ms）。

## 方法

### relay

`int relay()`

> 扫描并补发一批待投递消息（由 @Scheduled 周期触发）

**返回**: 本轮成功发送条数
