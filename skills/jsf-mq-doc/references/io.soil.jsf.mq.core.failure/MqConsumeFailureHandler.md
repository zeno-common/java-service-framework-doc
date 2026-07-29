# MqConsumeFailureHandler

> 消费失败处理器：封装失败落库与重放编排，屏蔽底层 MqConsumeFailureStore 细节

- **包**: io.soil.jsf.mq.core.failure

## 方法

### save

`void save(MqConsumeFailureRecord record)`

> 持久化失败记录。存储异常仅记日志不抛出，避免反噬消费线程

### replay

`int replay(int limit, Consumer<MqConsumeFailureRecord> replayer)`

> 重放待处理失败记录：fetchPending → 逐条交给 replayer；成功标记 REPLAYED，单条失败保持 PENDING 不影响其余

**参数**:
- `limit` (int) — 单次最大重放条数
- `replayer` (Consumer) — 业务重放逻辑（抛异常则该条保持 PENDING，下次可再重放）

**返回**: int — 成功重放条数

**示例**:
```java
// 需自行接入定时任务或管理端接口触发，框架不内置自动重放
@Scheduled(fixedDelay = 30_000)
public void replay() {
    int n;
    while ((n = failureHandler.replay(100, r -> bizService.reprocess(r.getPayload()))) > 0) {
        log.info("replayed {}", n);
    }
}
```

> 重放需保证业务幂等。
