# MqConsumerProperties

> 消费者侧配置属性，前缀 `jsf.mq.consumer`；NameServer 默认读取 rocketmq.name-server，未配置回退 127.0.0.1:9876

- **包**: io.soil.jsf.mq.config.properties
- **注解**: `@ConfigurationProperties(prefix = "jsf.mq.consumer")`

## 字段

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `nameServer` | String | 127.0.0.1:9876 | 消费者侧 RocketMQ NameServer（`@Value` 读取 `rocketmq.name-server` 回退） |
| `enabled` | boolean | true | 是否启用消费者（本地开发可关闭避免连接 RocketMQ）；设为 false 时 `MqConsumerAutoConfig` 与 `MqMongoConsumeAutoConfig` 整组不装配 |

## 配置示例

```yaml
jsf:
  mq:
    consumer:
      name-server: 127.0.0.1:9876   # 缺省复用 rocketmq.name-server
      enabled: true
```
