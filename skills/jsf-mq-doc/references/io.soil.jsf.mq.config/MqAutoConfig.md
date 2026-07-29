# 自动配置（拆分后的 3 个类）

> jsf-mq 原统一自动配置 `MqAutoConfig` 已按职责拆分为 3 个类，分别落在不同模块，全部基于接口条件装配（依赖倒置）。

- **包**: `io.soil.jsf.mq.config`
- **注解**: `@Configuration` + `@ConditionalOnClass(RocketMQTemplate.class)`（producer/consumer 侧）、`@EnableConfigurationProperties(MqProperties.class)`（common 侧）

## 装配规则

| 自动配置类 | 所在模块 | 条件 | 注册 Bean |
|-----------|----------|------|-----------|
| `MqPropertiesAutoConfig` | `jsf-mq-common` | 始终 | 配置属性 `MqProperties` |
| `MqProducerAutoConfig` | `jsf-mq-producer` | 始终 | `MqProducer` |
| `MqProducerAutoConfig` | `jsf-mq-producer` | 容器存在 `MqOutboxStore`（引入 jsf-mq-producer-mongodb） | `MqOutbox` + `MqOutboxRelay`（需 `@EnableScheduling`，relay 默认开启） |
| `MqConsumerAutoConfig` | `jsf-mq-consumer` | 容器存在 `MqConsumeFailureStore`（引入 jsf-mq-consumer-mongodb） | `MqConsumeFailureHandler` |

所有 Bean 均 `@ConditionalOnMissingBean`，业务可自定义实现覆盖。

## MongoDB 实现自动配置

可靠性组件的 MongoDB 实现同样按侧拆分，保证 Store Bean 先于核心装配：

| 自动配置类 | 所在模块 | 注册 Bean |
|-----------|----------|-----------|
| `MqMongoOutboxAutoConfig` | `jsf-mq-producer-mongodb` | `MqOutboxStore`（MongoMqOutboxStore） |
| `MqMongoConsumeAutoConfig` | `jsf-mq-consumer-mongodb` | `MqIdempotentStore`（MongoMqIdempotentStore）、`MqConsumeFailureStore`（MongoMqConsumeFailureStore） |

二者均标注 `@AutoConfigureBefore` 对应核心自动配置类，使核心的 `@ConditionalOnBean(XxxStore.class)` 条件成立。
