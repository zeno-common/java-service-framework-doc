# MqConsumeFailureStore

> 消费失败记录存储接口（依赖倒置：核心定义协议，落库由实现模块提供，如 jsf-mq-mongodb）

- **包**: io.soil.jsf.mq.core.failure

## 方法

### save

`void save(MqConsumeFailureRecord record)`

> 持久化失败记录，实现方须回填 `MqConsumeFailureRecord#setId(Long)`

### fetchPending

`List<MqConsumeFailureRecord> fetchPending(int limit)`

> 拉取待重放（PENDING）记录，按失败时间升序

### markReplayed

`void markReplayed(Long id)`

> 标记记录为已重放（REPLAYED）
