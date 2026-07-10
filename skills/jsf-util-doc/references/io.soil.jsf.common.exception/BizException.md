# BizException

> 业务异常，用于表示违反业务规则（如前置条件不满足、状态机流转非法），由 Domain / App 层抛出

- **包**: io.soil.jsf.common.exception
- **父类**: `BaseException`
- **异常类型**: `ExceptionType.BIZ`

## 说明

`BizException` 继承自 `BaseException`，`type()` 固定返回 `ExceptionType.BIZ`。当它在 COLA 5 分层架构的 Domain / App 层被抛出后，由 Web 层的全局异常处理器统一捕获，转换为标准错误响应（`errType = BIZ`，`errCode = 异常自定义码`，`errDesc = 异常消息`）。

推荐通过 `of(Error, Object...)` 静态工厂方法创建实例，配合实现 `Error` 接口的枚举使用，避免硬编码错误码与描述。

## 静态方法

### of

`static BizException of(Error error, Object... descArgs)`

> 根据错误定义和描述参数构造业务异常（无原始原因）

**参数**:
- `error` (`Error`) — 错误定义（提供 code 和 desc 模板）
- `descArgs` (`Object...`) — 描述模板参数（MessageFormat 格式化）

**返回**: `BizException` — 业务异常实例

### of (with cause)

`static BizException of(Throwable cause, Error error, Object... descArgs)`

> 根据错误定义、原始原因和描述参数构造业务异常

**参数**:
- `cause` (`Throwable`) — 原始异常原因
- `error` (`Error`) — 错误定义（提供 code 和 desc 模板）
- `descArgs` (`Object...`) — 描述模板参数（MessageFormat 格式化）

**返回**: `BizException` — 业务异常实例

## 构造

| 签名 | 说明 |
|------|------|
| `BizException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 全参数构造（protected） |

## 方法

### type

`ExceptionType type()`

> 获取异常类型

**返回**: `ExceptionType` — 固定返回 `ExceptionType.BIZ`

## 示例

```java
// 定义领域错误码枚举
public enum OrderError implements Error {
    NOT_FOUND("ORDER-NOT-FOUND", "订单 {0} 不存在"),
    EXISTED("ORDER-EXISTED", "订单已存在");

    private final String code;
    private final String desc;
    OrderError(String code, String desc) { this.code = code; this.desc = desc; }
    @Override public String code() { return code; }
    @Override public String desc() { return desc; }
}

// 通过 Error 枚举构造（推荐）
throw BizException.of(OrderError.NOT_FOUND, orderId);

// 带原始异常
throw BizException.of(cause, OrderError.NOT_FOUND, orderId);
```