# BizException

> 业务异常，用于表示违反业务规则（如前置条件不满足、状态机流转非法），由 Domain / App 层抛出

- **包**: io.soil.jsf.common.exception
- **父类**: `BaseException`
- **异常类型**: `ExceptionType.BIZ`

## 说明

`BizException` 继承自 `BaseException`，`type()` 固定返回 `ExceptionType.BIZ`。当它在 COLA 5 分层架构的 Domain / App 层被抛出后，由 Web 层的全局异常处理器统一捕获，转换为标准错误响应（`errType = BIZ`，`errCode = 异常自定义码`，`errDesc = 异常消息`）。

## 静态方法

### of

`static BizException of(ErrorDefine errorDefine)`

> 根据错误定义创建业务异常

**参数**:
- `errorDefine` (`ErrorDefine`) — 错误定义，提供异常码和消息

**返回**: `BizException` — 业务异常对象

### of

`static BizException of(ErrorDefine errorDefine, Throwable throwable)`

> 根据错误定义创建业务异常，可附带原始异常

**参数**:
- `errorDefine` (`ErrorDefine`) — 错误定义，提供异常码和消息
- `throwable` (`Throwable`) — 原始异常，可为 null

**返回**: `BizException` — 业务异常对象

## 构造

| 签名 | 说明 |
|------|------|
| `BizException(String msg)` | 使用消息构造 |
| `BizException(String msgPattern, Object... msgArgs)` | 使用消息模板（MessageFormat）构造 |
| `BizException(Throwable throwable)` | 使用原始异常构造，消息取 `throwable.getMessage()` |
| `BizException(Throwable throwable, String msg)` | 使用原始异常与消息构造 |
| `BizException(Throwable throwable, String msgPattern, Object... msgArgs)` | 使用原始异常与消息模板构造 |
| `BizException(String code, Throwable throwable)` | 使用自定义异常码与原始异常构造，消息取 `throwable.getMessage()` |
| `BizException(String code, Throwable throwable, String msg)` | 使用自定义异常码、原始异常与消息构造 |
| `BizException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 使用自定义异常码、原始异常与消息模板构造 |

## 方法

### type

`ExceptionType type()`

> 获取异常类型

**返回**: `ExceptionType` — 固定返回 `ExceptionType.BIZ`

## 示例

```java
// 使用 ErrorDefine 枚举
throw BizException.of(OrderError.NOT_FOUND);

// 使用 ErrorDefine 枚举 + 原始异常
throw BizException.of(OrderError.NOT_FOUND, cause);

// 定义领域专属子类
public class OrderException extends BizException {
    public OrderException(String msg) { super("ORDER-ERROR", msg); }
    public OrderException(String code, String msg) { super(code, msg); }
}

// 使用消息模板
throw new OrderException("ORDER-NOT-FOUND", "订单 {0} 不存在", orderId);

// 包装原始异常
throw new BizException("DB-ERROR", cause, "操作失败");
```