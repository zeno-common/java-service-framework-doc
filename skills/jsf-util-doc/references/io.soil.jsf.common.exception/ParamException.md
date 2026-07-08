# ParamException

> 参数校验异常，用于表示请求入参不合法（如非空、格式校验失败），由 Adapter 层在参数校验时抛出

- **包**: io.soil.jsf.common.exception
- **父类**: `BaseException`
- **异常类型**: `ExceptionType.PARAM`

## 说明

`ParamException` 继承自 `BaseException`，`type()` 固定返回 `ExceptionType.PARAM`。当它被抛出后，由全局异常处理器 `RestGlobalExceptionResolver` 的 `handleValidationException(ParamException)` 统一捕获，返回 HTTP 400 的标准错误响应（`errType = PARAM`，`errCode = 异常自定义码`，`errDesc = 异常消息`）。

构造方法为 `protected`，仅允许同包类或子类实例化；业务代码通常定义领域专属子类后抛出，或通过框架校验流程触发。

## 构造

| 签名 | 说明 |
|------|------|
| `ParamException(String msg)` | 使用消息构造 |
| `ParamException(String msgPattern, Object... msgArgs)` | 使用消息模板（MessageFormat）构造 |
| `ParamException(Throwable throwable, String msg)` | 使用原始异常与消息构造 |
| `ParamException(Throwable throwable)` | 使用原始异常构造，消息取 `throwable.getMessage()` |
| `ParamException(Throwable throwable, String msgPattern, Object... msgArgs)` | 使用原始异常与消息模板构造 |
| `ParamException(String code, String msg)` | 使用自定义异常码与消息构造 |
| `ParamException(String code, Throwable throwable, String msg)` | 使用自定义异常码、原始异常与消息构造 |
| `ParamException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 使用自定义异常码、原始异常与消息模板构造 |

## 方法

### type

`ExceptionType type()`

> 获取异常类型

**返回**: `ExceptionType` — 固定返回 `ExceptionType.PARAM`

## 示例

```java
// 定义领域专属子类（构造方法为 protected，需通过子类实例化）
public class UserParamException extends ParamException {
    public UserParamException(String msg) { super(msg); }
    public UserParamException(String pattern, Object... args) { super(pattern, args); }
}

// 使用消息模板
throw new UserParamException("参数 {0} 不合法", paramName);

// 由全局异常处理器自动映射为 HTTP 400 + RestExceptionResponse
// errType = PARAM, errCode = 异常自定义码, errDesc = 异常消息
```