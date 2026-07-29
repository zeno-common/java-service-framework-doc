# MqAutoConfig

> jsf-mq 自动配置：classpath 存在 RocketMQTemplate 时激活，注册 MqProducer 与 MqProperties；按 Store Bean 存在性条件装配可靠性组件

- **包**: io.soil.jsf.mq.config
- **注解**: @Configuration @ConditionalOnClass(RocketMQTemplate.class) @EnableConfigurationProperties(MqProperties.class)

## 装配规则

| 条件 | 注册 Bean |
|------|-----------|
| 始终 | `MqProducer`（mqProducer） |
| 容器存在 `MqOutboxStore` | `MqOutbox` + `MqOutboxRelay`（需 @EnableScheduling，relay 默认开启） |
| 容器存在 `MqConsumeFailureStore` | `MqConsumeFailureHandler` |

所有 Bean 均 `@ConditionalOnMissingBean`，业务可自定义实现覆盖。
