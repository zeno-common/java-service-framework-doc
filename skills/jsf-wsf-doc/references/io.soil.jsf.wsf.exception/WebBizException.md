# WebBizException

> Web 业务异常，可指定 HTTP 状态码的业务异常，用于 application layer 层的异常响应场景。本类为 final，不可被继承

- **包**: io.soil.jsf.wsf.exception
- **父类**: `BizException`（io.soil.jsf.common.exception）
- **修饰**: `final`
- **异常类型**: `ExceptionType.BIZ`

## 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `status` | `HttpStatus` | HTTP 状态码 |

## 静态方法

### of (Error)

`static WebBizException of(HttpStatus status, Error error, Object... descArgs)`

> 基于 Error 错误码枚举构造 WebBizException，并指定 HTTP 状态码

**参数**:
- `status` (`HttpStatus`) — HTTP 状态码
- `error` (`Error`) — 错误定义（提供 code 和 desc 模板）
- `descArgs` (`Object...`) — 描述模板参数（MessageFormat 格式化）

**返回**: `WebBizException` — Web 业务异常实例

### of (Error with cause)

`static WebBizException of(HttpStatus status, Throwable cause, Error error, Object... descArgs)`

> 基于错误定义、原始原因和描述参数构造 WebBizException，并指定 HTTP 状态码

**参数**:
- `status` (`HttpStatus`) — HTTP 状态码
- `cause` (`Throwable`) — 原始异常原因
- `error` (`Error`) — 错误定义（提供 code 和 desc 模板）
- `descArgs` (`Object...`) — 描述模板参数（MessageFormat 格式化）

**返回**: `WebBizException` — Web 业务异常实例

### of (BizException)

`static WebBizException of(HttpStatus status, BizException e)`

> 将已有 BizException 重新包装为 WebBizException，保留原始异常码与消息，仅补充 HTTP 状态码

**参数**:
- `status` (`HttpStatus`) — HTTP 状态码
- `e` (`BizException`) — 原始业务异常

**返回**: `WebBizException` — 包装后的 Web 业务异常对象

## 构造

| 签名 | 说明 |
|------|------|
| `WebBizException(HttpStatus status, String code, String msg)` | 指定 HTTP 状态码、自定义异常状态码和消息内容构造 |
| `WebBizException(HttpStatus status, String code, String msgPattern, Object... msgArgs)` | 指定 HTTP 状态码、自定义异常状态码和消息模板构造 |
| `WebBizException(HttpStatus status, String code, Throwable throwable)` | 指定 HTTP 状态码、自定义异常状态码和异常栈构造，消息取 throwable.getMessage() |
| `WebBizException(HttpStatus status, String code, Throwable throwable, String msg)` | 指定 HTTP 状态码、自定义异常状态码、异常栈和消息内容构造 |
| `WebBizException(HttpStatus status, String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 全参数构造 |

## 方法

### status

`HttpStatus status()`

> 获取 HTTP 状态码

**返回**: `HttpStatus` — HTTP 状态码

## 示例

```java
// 通过 Error 枚举 + HTTP 状态码构造（推荐）
throw WebBizException.of(HttpStatus.NOT_FOUND, OrderError.NOT_FOUND, orderId);

// 带原始异常
throw WebBizException.of(HttpStatus.INTERNAL_SERVER_ERROR, cause, DbError.SAVE_FAILED);

// 将 BizException 重新包装为 WebBizException
WebBizException wrapped = WebBizException.of(HttpStatus.BAD_REQUEST, bizEx);
throw wrapped;

// 直接使用构造函数
throw new WebBizException(HttpStatus.BAD_REQUEST, "PARAM_ERROR", "参数错误");
throw new WebBizException(HttpStatus.BAD_REQUEST, "PARAM_INVALID", "参数 {0} 不能为空", "name");
```