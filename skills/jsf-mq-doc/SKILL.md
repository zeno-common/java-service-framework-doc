---
name: "jsf-mq-doc"
description: "Use when coding with jsf-mq SDK, need API reference for RocketMQ unified producer, consumer base class, outbox reliable delivery, consume idempotency, and consume failure replay."
---

# jsf-mq SDK 参考

基于 RocketMQ 5.5 封装的通用消息中间件模块：统一生产者 API、消费者基类（三态结果 + 可选幂等）、Outbox 可靠发送、消费失败落库与重放。

## 依赖引入

Maven 工程的依赖引入参考：'[jsf-bom-doc/SKILL.md](../jsf-bom-doc/SKILL.md)'

| ArtifactId | 说明 |
|-----------|------|
| `jsf-mq-core` | 生产者与消费者核心：统一生产者 API、Outbox 可靠发送、消费者基类、失败落库重放、幂等抽象 |
| `jsf-mq-mongodb` | 可靠性 MongoDB 实现（Outbox / 幂等 / 失败记录的 Store） |

> 仅引入 `jsf-mq-core` 即可发/收消息；引入 `jsf-mq-mongodb` 后，`MqOutbox` / `MqOutboxRelay` / `MqConsumeFailureHandler` 才会被条件装配（见各自动配置类）。

## 类索引

### 核心 API

| 类 | 包 | 说明 | 文档 |
|----|-----|------|------|
| `MqProducer` | `io.soil.jsf.mq.core` | 统一消息生产者（同步/异步/单向/延迟） | [MqProducer](references/io.soil.jsf.mq.core/MqProducer.md) |
| `AbstractMqConsumer` | `io.soil.jsf.mq.core` | 消费者基类，三态结果 + 可选幂等 | [AbstractMqConsumer](references/io.soil.jsf.mq.core/AbstractMqConsumer.md) |
| `ConsumeStatus` | `io.soil.jsf.mq.core` | 消费结果三态枚举 | [ConsumeStatus](references/io.soil.jsf.mq.core/ConsumeStatus.md) |

### 可靠发送（Outbox）

| 类 | 包 | 说明 | 文档 |
|----|-----|------|------|
| `MqOutbox` | `io.soil.jsf.mq.core.outbox` | Outbox 编排入口：事务内落库 + 提交后投递 + relay 兜底 | [MqOutbox](references/io.soil.jsf.mq.core.outbox/MqOutbox.md) |
| `MqOutboxRelay` | `io.soil.jsf.mq.core.outbox` | 兜底补发器（定时扫描待投递行） | [MqOutboxRelay](references/io.soil.jsf.mq.core.outbox/MqOutboxRelay.md) |
| `MqOutboxMessage` | `io.soil.jsf.mq.core.outbox` | Outbox 消息 POJO | [MqOutboxMessage](references/io.soil.jsf.mq.core.outbox/MqOutboxMessage.md) |
| `MqOutboxStore` | `io.soil.jsf.mq.core.outbox` | Outbox 存储接口（依赖倒置） | [MqOutboxStore](references/io.soil.jsf.mq.core.outbox/MqOutboxStore.md) |
| `MqOutboxStatus` | `io.soil.jsf.mq.core.outbox` | Outbox 状态枚举 | [MqOutboxStatus](references/io.soil.jsf.mq.core.outbox/MqOutboxStatus.md) |

### 消费幂等

| 类 | 包 | 说明 | 文档 |
|----|-----|------|------|
| `MqIdempotentStore` | `io.soil.jsf.mq.core.idempotent` | 消费幂等存储接口（claim/markProcessed/release） | [MqIdempotentStore](references/io.soil.jsf.mq.core.idempotent/MqIdempotentStore.md) |

### 消费失败兜底

| 类 | 包 | 说明 | 文档 |
|----|-----|------|------|
| `MqConsumeFailureHandler` | `io.soil.jsf.mq.core.failure` | 失败落库 + 重放编排 | [MqConsumeFailureHandler](references/io.soil.jsf.mq.core.failure/MqConsumeFailureHandler.md) |
| `MqConsumeFailureRecord` | `io.soil.jsf.mq.core.failure` | 失败记录 POJO | [MqConsumeFailureRecord](references/io.soil.jsf.mq.core.failure/MqConsumeFailureRecord.md) |
| `MqConsumeFailureStore` | `io.soil.jsf.mq.core.failure` | 失败记录存储接口 | [MqConsumeFailureStore](references/io.soil.jsf.mq.core.failure/MqConsumeFailureStore.md) |
| `MqConsumeFailureStatus` | `io.soil.jsf.mq.core.failure` | 失败记录状态枚举 | [MqConsumeFailureStatus](references/io.soil.jsf.mq.core.failure/MqConsumeFailureStatus.md) |

### 配置与装配

| 类 | 包 | 说明 | 文档 |
|----|-----|------|------|
| `MqProducerProperties` | `io.soil.jsf.mq.config.properties` | 生产者侧配置属性（前缀 `jsf.mq.producer`，含 outbox 段） | [MqProducerProperties](references/io.soil.jsf.mq.config.properties/MqProducerProperties.md) |
| `MqConsumerProperties` | `io.soil.jsf.mq.config.properties` | 消费者侧配置属性（前缀 `jsf.mq.consumer`） | [MqConsumerProperties](references/io.soil.jsf.mq.config.properties/MqConsumerProperties.md) |
| `MqProducerAutoConfig` | `io.soil.jsf.mq.config` | 生产者自动配置（注册 MqProducer / MqOutbox / MqOutboxRelay） | [MqProducerAutoConfig](references/io.soil.jsf.mq.config/MqProducerAutoConfig.md) |
| `MqConsumerAutoConfig` | `io.soil.jsf.mq.config` | 消费者自动配置（注册 MqConsumeFailureHandler） | [MqConsumerAutoConfig](references/io.soil.jsf.mq.config/MqConsumerAutoConfig.md) |
| `MqProducerException` | `io.soil.jsf.mq.exception` | 生产者侧异常（发送失败 / 生产者不可用） | [MqProducerException](references/io.soil.jsf.mq.exception/MqProducerException.md) |
| `MqConsumerException` | `io.soil.jsf.mq.exception` | 消费者侧异常（消费失败，触发 broker 重试） | [MqConsumerException](references/io.soil.jsf.mq.exception/MqConsumerException.md) |

