# SysException

> 系统异常，用于表示基础设施层捕获并包装的技术异常（如数据库访问失败、外部服务调用异常），由 Infrastructure 层抛出

- **包**: io.soil.jsf.common.exception
- **父类**: `BaseException`
- **异常类型**: `ExceptionType.SYS`

## 说明

`SysException` 继承自 `BaseException`，`type()` 固定返回 `ExceptionType.SYS`。当它在 COLA 5 分层架构的 Infrastructure 层将底层技术异常包装后抛出，由 Web 层的全局异常处理器统一捕获，转换为标准错误响应（`errType = SYS`，`errCode = 异常自定义码`，`errDesc = 异常消息`），且不向前端暴露底层技术细节。

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