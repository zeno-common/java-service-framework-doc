# MqProducerAutoConfig

> 生产者侧自动配置：注册统一生产者与 Outbox 可靠发送编排 / 兜底 relay，全部基于接口条件装配（依赖倒置）

- **包**: io.soil.jsf.mq.config
- **注解**: `@Configuration` + `@ConditionalOnClass(RocketMQTemplate.class)` + `@EnableConfigurationProperties(MqProducerProperties.class)`

## 注册 Bean

| Bean | 条件 | 说明 |
|------|------|------|
| `mqProducer` | 始终（`@ConditionalOnMissingBean`） | 统一消息生产者 |
| `mqOutbox` | 容器存在 `MqOutboxStore`（引入 jsf-mq-producer-mongodb） | Outbox 编排入口（事务内落库 + 提交后立即投递） |
| `mqOutboxRelay` | 容器存在 `MqOutbox` 且 `jsf.mq.producer.outbox.relay.enabled` 非 false | Outbox 兜底补发器（需应用 `@EnableScheduling`） |

所有 Bean 均 `@ConditionalOnMissingBean`，业务可自定义实现覆盖。
