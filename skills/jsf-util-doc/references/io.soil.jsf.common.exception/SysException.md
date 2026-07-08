# SysException

> 系统异常，用于表示基础设施层捕获并包装的技术异常（如数据库访问失败、外部服务调用异常），由 Infrastructure 层抛出

- **包**: io.soil.jsf.common.exception
- **父类**: `BaseException`
- **异常类型**: `ExceptionType.SYS`

## 说明

`SysException` 继承自 `BaseException`，`type()` 固定返回 `ExceptionType.SYS`。当它在 COLA 5 分层架构的 Infrastructure 层将底层技术异常包装后抛出，由 Web 层的全局异常处理器统一捕获，转换为标准错误响应（`errType = SYS`，`errCode = 异常自定义码`，`errDesc = 异常消息`），且不向前端暴露底层技术细节。

## 静态方法

### of

`static SysException of(ErrorDefine errorDefine, Object... msgArgs)`

> 根据错误定义创建系统异常

**参数**:
- `errorDefine` (`ErrorDefine`) — 错误定义，提供异常码和消息模板
- `msgArgs` (`Object...`) — 消息模板参数，用于 `MessageFormat.format` 格式化

**返回**: `SysException` — 系统异常对象

### of

`static SysException of(Throwable throwable, ErrorDefine errorDefine, Object... msgArgs)`

> 根据错误定义创建系统异常，可附带原始异常

**参数**:
- `throwable` (`Throwable`) — 原始异常，可为 null
- `errorDefine` (`ErrorDefine`) — 错误定义，提供异常码和消息模板
- `msgArgs` (`Object...`) — 消息模板参数，用于 `MessageFormat.format` 格式化

**返回**: `SysException` — 系统异常对象

## 构造

| 签名 | 说明 |
|------|------|
| `SysException(String msg)` | 使用消息构造 |
| `SysException(String msgPattern, Object... msgArgs)` | 使用消息模板（MessageFormat）构造 |
| `SysException(Throwable throwable)` | 使用原始异常构造，消息取 `throwable.getMessage()` |
| `SysException(Throwable throwable, String msg)` | 使用原始异常与消息构造 |
| `SysException(Throwable throwable, String msgPattern, Object... msgArgs)` | 使用原始异常与消息模板构造 |
| `SysException(String code, Throwable throwable)` | 使用自定义异常码与原始异常构造，消息取 `throwable.getMessage()` |
| `SysException(String code, Throwable throwable, String msg)` | 使用自定义异常码、原始异常与消息构造 |
| `SysException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 使用自定义异常码、原始异常与消息模板构造 |

## 方法

### type

`ExceptionType type()`

> 获取异常类型

**返回**: `ExceptionType` — 固定返回 `ExceptionType.SYS`

## 示例

```java
// 使用 ErrorDefine 枚举
throw SysException.of(SysError.BUSY);

// 使用 ErrorDefine 枚举 + 消息模板参数
throw SysException.of(SysError.TIMEOUT, serviceName);

// 使用 ErrorDefine 枚举 + 原始异常
throw SysException.of(cause, SysError.DB);

// 直接使用
throw new SysException("系统繁忙");

// 包装底层技术异常
try {
    // ...
} catch (SQLException e) {
    throw new SysException("DB-SAVE-FAILED", e, "数据库访问失败");
}

// 使用消息模板
throw new SysException("服务 {0} 调用超时", serviceName);
```