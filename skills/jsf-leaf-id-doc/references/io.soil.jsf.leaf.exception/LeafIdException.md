# LeafIdException

> Leaf ID 生成器异常，封装时钟回拨/workerId 越界/抢占失败等错误

- **包**: io.soil.jsf.leaf.exception
- **父类**: `BaseException`
- **异常类型**: `ExceptionType.SYS`

## 说明

`LeafIdException` 继承自 `BaseException`，`type()` 固定返回 `ExceptionType.SYS`。封装 ID 生成过程中的各类错误，包括但不限于：
- 时钟回拨超过容忍阈值（> 5ms）
- workerId 超出合法范围（0 ~ 255）
- 无可用 workerId（所有 worker 均被占用）
- 乐观锁抢占 worker 失败

## 构造

| 签名 | 说明 |
|------|------|
| `LeafIdException(String msg)` | 使用消息构造 |
| `LeafIdException(String msgPattern, Object... msgArgs)` | 使用消息模板（MessageFormat）构造 |
| `LeafIdException(Throwable throwable, String msg)` | 使用原始异常与消息构造 |

## 方法

### type

`ExceptionType type()`

> 获取异常类型

**返回**: `ExceptionType` — 固定返回 `ExceptionType.SYS`

## 示例

```java
// 时钟回拨场景（由 LeafIdGenImpl 内部抛出）
// 回拨 > 5ms 时：
// throw new LeafIdException("Leaf Id nextId 异常，最后时间戳({})大于当前时间戳({})", lastTimestamp, timestamp);

// workerId 越界场景
// throw new LeafIdException("workerID must gte 0 and lt {0}", MAXIMUM_WORKER);
```