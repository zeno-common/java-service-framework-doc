# WebBizException

> Web 业务异常，继承 BizException，在业务异常基础上额外持有 HTTP 状态码，由全局异常处理器按异常对象自带的状态码返回对应的 HTTP 响应

- **包**: io.soil.jsf.wsf.exception
- **父类**: `BizException`（io.soil.jsf.common.exception）
- **异常类型**: `ExceptionType.BIZ`

## 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `status` | `HttpStatus` | HTTP 状态码 |

## 静态方法

### rethrow

`static void rethrow(HttpStatus status, BizException e)`

> 将业务异常重新包装为 Web 业务异常并抛出，保留原始异常码和消息，同时指定 HTTP 状态码

**参数**:
- `status` (`HttpStatus`) — HTTP 状态码
- `e` (`BizException`) — 原始业务异常

## 构造

| 签名 | 说明 |
|------|------|
| `WebBizException(String msg)` | 使用消息构造，默认 HTTP 500 |
| `WebBizException(String msgPattern, Object... msgArgs)` | 使用消息模板构造，默认 HTTP 500 |
| `WebBizException(HttpStatus status, String msg)` | 使用 HTTP 状态码和消息构造 |
| `WebBizException(HttpStatus status, String msgPattern, Object... msgArgs)` | 使用 HTTP 状态码和消息模板构造 |
| `WebBizException(String code, HttpStatus status, String msg)` | 使用自定义错误码、HTTP 状态码和消息构造 |
| `WebBizException(String code, HttpStatus status, String msgPattern, Object... msgArgs)` | 使用自定义错误码、HTTP 状态码和消息模板构造 |
| `WebBizException(Throwable throwable)` | 使用异常栈构造，默认 HTTP 500 |
| `WebBizException(String code, Throwable throwable)` | 使用自定义错误码和异常栈构造 |
| `WebBizException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 使用自定义错误码、异常栈和消息模板构造，默认 HTTP 500 |
| `WebBizException(String code, HttpStatus status, Throwable throwable, String msgPattern, Object... msgArgs)` | 全参数构造 |

## 方法

### type

`ExceptionType type()`

> 获取异常类型

**返回**: `ExceptionType` — 固定返回 `ExceptionType.BIZ`

### status

`HttpStatus status()`

> 获取 HTTP 状态码

**返回**: `HttpStatus` — HTTP 状态码

## 示例

```java
// 简单消息异常（HTTP 500）
throw new WebBizException("操作失败");

// 指定 HTTP 状态码
throw new WebBizException(HttpStatus.BAD_REQUEST, "参数错误");

// 自定义错误码 + HTTP 状态码
throw new WebBizException("USER_NOT_FOUND", HttpStatus.NOT_FOUND, "用户不存在");

// 消息模板
throw new WebBizException(HttpStatus.BAD_REQUEST, "参数 {0} 不能为空", "name");

// 包装原始异常
throw new WebBizException("DB_ERROR", throwable);

// 将 BizException 重新包装为 WebBizException 并抛出
WebBizException.rethrow(HttpStatus.BAD_REQUEST, bizEx);
```