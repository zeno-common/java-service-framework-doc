# MqConsumerAutoConfig

> 消费者侧自动配置：注册消费失败处理器（DISCARD 落库 + 重放编排），基于接口条件装配（依赖倒置）

- **包**: io.soil.jsf.mq.config
- **注解**: `@Configuration` + `@ConditionalOnClass(RocketMQTemplate.class)` + `@EnableConfigurationProperties(MqConsumerProperties.class)`

## 注册 Bean

| Bean | 条件 | 说明 |
|------|------|------|
| `mqConsumeFailureHandler` | 容器存在 `MqConsumeFailureStore`（引入 jsf-mq-consumer-mongodb） | 消费失败处理（落库 + 重放） |

Bean 标注 `@ConditionalOnMissingBean`，业务可自定义实现覆盖。
