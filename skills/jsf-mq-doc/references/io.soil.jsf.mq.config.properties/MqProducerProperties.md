# MqProducerProperties

> 生产者侧配置属性，前缀 `jsf.mq.producer`；NameServer 默认读取 rocketmq.name-server，未配置回退 127.0.0.1:9876

- **包**: io.soil.jsf.mq.config.properties
- **注解**: `@ConfigurationProperties(prefix = "jsf.mq.producer")`

## 字段

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `nameServer` | String | 127.0.0.1:9876 | 生产者侧 RocketMQ NameServer（`@Value` 读取 `rocketmq.name-server` 回退） |
| `group` | String | jsf-mq-producer | 默认生产者组 |
| `outbox.immediateSend` | boolean | true | 事务提交后立即投递（false 则纯 relay 轮询） |
| `outbox.maxAttempts` | int | 16 | 最大发送尝试，耗尽后置 FAILED（人工介入） |
| `outbox.lockSeconds` | long | 60 | 认领锁时长（秒），SENDING 超时视为僵尸行 |
| `outbox.initialBackoffSeconds` | long | 10 | 首次退避（秒），同时作为 insert 时 relay 缓冲 |
| `outbox.maxBackoffSeconds` | long | 3600 | 退避上限（秒） |
| `outbox.relay.enabled` | boolean | true | relay 兜底开关（需 `@EnableScheduling`） |
| `outbox.relay.interval` | long | 5000 | 扫描间隔（毫秒） |
| `outbox.relay.batchSize` | int | 100 | 单轮扫描批量 |

## 配置示例

```yaml
jsf:
  mq:
    producer:
      name-server: 127.0.0.1:9876   # 缺省复用 rocketmq.name-server
      group: jsf-mq-producer
      outbox:
        immediate-send: true
        max-attempts: 16
        relay:
          enabled: true
          interval: 5000
```
