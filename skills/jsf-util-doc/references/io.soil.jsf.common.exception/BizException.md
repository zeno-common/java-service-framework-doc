# BizException

> 业务异常，用于表示违反业务规则（如前置条件不满足、状态机流转非法），由 Domain / App 层抛出

- **包**: io.soil.jsf.common.exception
- **父类**: `BaseException`
- **异常类型**: `ExceptionType.BIZ`

## 说明

`BizException` 继承自 `BaseException`，`type()` 固定返回 `ExceptionType.BIZ`。当它在 COLA 5 分层架构的 Domain / App 层被抛出后，由 Web 层的全局异常处理器统一捕获，转换为标准错误响应（`errType = BIZ`，`errCode = 异常自定义码`，`errDesc = 异常消息`）。

构造方法为 `protected`，仅允许同包类或子类实例化；业务代码通常定义领域专属子类后抛出，而非直接 `new`。

## 构造

| 签名 | 说明 |
|------|------|
| `BizException(String msg)` | 使用消息构造 |
| `BizException(String msgPattern, Object... msgArgs)` | 使用消息模板（MessageFormat）构造 |
| `BizException(Throwable throwable, String msg)` | 使用原始异常与消息构造 |
| `BizException(Throwable throwable)` | 使用原始异常构造，消息取 `throwable.getMessage()` |
| `BizException(Throwable throwable, String msgPattern, Object... msgArgs)` | 使用原始异常与消息模板构造 |
| `BizException(String code, String msg)` | 使用自定义异常码与消息构造 |
| `BizException(String code, Throwable throwable, String msg)` | 使用自定义异常码、原始异常与消息构造 |
| `BizException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 使用自定义异常码、原始异常与消息模板构造 |

## 方法

### type

`ExceptionType type()`

> 获取异常类型

**返回**: `ExceptionType` — 固定返回 `ExceptionType.BIZ`

## 示例

```java
// 定义领域专属子类（构造方法为 protected，需通过子类实例化）
public class OrderException extends BizException {
    public OrderException(String msg) { super(msg); }
    public OrderException(String pattern, Object... args) { super(pattern, args); }
}

// 使用消息模板
throw new OrderException("订单 {0} 不存在", orderId);

// 包装原始异常
throw new OrderException(cause, "操作失败");
```
