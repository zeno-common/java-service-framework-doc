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
| `jsf-mq-common` | 共享基础：统一异常、配置属性（被 producer/consumer 传递依赖，通常无需显式声明） |
| `jsf-mq-producer` | 生产者侧：统一生产者 API、Outbox 可靠发送 |
| `jsf-mq-consumer` | 消费者侧：消费者基类、失败落库重放、幂等抽象 |
| `jsf-mq-producer-mongodb` | 生产者可靠性 MongoDB 实现（Outbox 的 Store） |
| `jsf-mq-consumer-mongodb` | 消费者可靠性 MongoDB 实现（幂等 / 失败记录的 Store） |

> 仅引入 `jsf-mq-producer` + `jsf-mq-consumer` 也能发/收消息；引入对应 `jsf-mq-*-mongodb` 后，`MqOutbox` / `MqOutboxRelay` / `MqConsumeFailureHandler` 才会被条件装配（见各自动配置类）。

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
| `MqProperties` | `io.soil.jsf.mq.config.properties` | 配置属性（`jsf.mq` 前缀） | [MqProperties](references/io.soil.jsf.mq.config.properties/MqProperties.md) |
| `MqProducerAutoConfig` / `MqConsumerAutoConfig` / `MqPropertiesAutoConfig` | `io.soil.jsf.mq.config` | 自动配置（按 Store Bean 条件装配，分别位于 jsf-mq-producer / jsf-mq-consumer / jsf-mq-common） | [MqAutoConfig](references/io.soil.jsf.mq.config/MqAutoConfig.md) |
| `MqException` | `io.soil.jsf.mq.exception` | 统一异常（发送/消费失败） | [MqException](references/io.soil.jsf.mq.exception/MqException.md) |

