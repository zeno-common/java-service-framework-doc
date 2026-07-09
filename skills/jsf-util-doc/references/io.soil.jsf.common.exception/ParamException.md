# ParamException

> 参数校验异常，用于表示请求入参不合法（如非空、格式校验失败等），由 Adapter 层在参数校验时抛出

- **包**: io.soil.jsf.common.exception
- **父类**: `BaseException`
- **修饰**: `final`
- **异常类型**: `ExceptionType.PARAM`

## 说明

`ParamException` 继承自 `BaseException`，`type()` 固定返回 `ExceptionType.PARAM`。当它在 COLA 5 分层架构的 Adapter 层被抛出后，由 Web 层的全局异常处理器统一捕获，转换为标准错误响应（`errType = PARAM`，`errCode = 异常自定义码`，`errDesc = 异常消息`）。

## 构造

| 签名 | 说明 |
|------|------|
| `ParamException(String msg)` | 使用消息构造 |
| `ParamException(String msgPattern, Object... msgArgs)` | 使用消息模板（MessageFormat）构造 |
| `ParamException(Throwable throwable)` | 使用原始异常构造，消息取 `throwable.getMessage()` |
| `ParamException(Throwable throwable, String msg)` | 使用原始异常与消息构造 |
| `ParamException(Throwable throwable, String msgPattern, Object... msgArgs)` | 使用原始异常与消息模板构造 |
| `ParamException(String code, Throwable throwable)` | 使用自定义异常码与原始异常构造 |
| `ParamException(String code, Throwable throwable, String msg)` | 使用自定义异常码、原始异常与消息构造 |
| `ParamException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 使用自定义异常码、原始异常与消息模板构造 |

## 方法

### type

`ExceptionType type()`

> 获取异常类型

**返回**: `ExceptionType` — 固定返回 `ExceptionType.PARAM`

## 示例

```java
// 直接使用
throw new ParamException("参数不能为空");

// 使用消息模板
throw new ParamException("参数 {0} 不合法", paramName);

// 包装原始异常
throw new ParamException(cause, "参数解析失败");

// 自定义异常码
throw new ParamException("USER-PARAM-INVALID", cause, "用户参数错误");
```
