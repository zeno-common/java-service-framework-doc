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

### of

`static WebBizException of(BizException e, HttpStatus status)`

> 将业务异常重新包装为 Web 业务异常，保留原始异常码和消息，同时指定 HTTP 状态码

**参数**:
- `e` (`BizException`) — 原始业务异常
- `status` (`HttpStatus`) — HTTP 状态码

**返回**: `WebBizException` — 包装后的 Web 业务异常对象

## 构造

| 签名 | 说明 |
|------|------|
| `WebBizException(HttpStatus status, String msg)` | 使用 HTTP 状态码和消息构造，code 取 status.name() |
| `WebBizException(HttpStatus status, String msgPattern, Object... msgArgs)` | 使用 HTTP 状态码和消息模板构造，code 取 status.name() |
| `WebBizException(HttpStatus status, String code, String msg)` | 使用 HTTP 状态码、自定义错误码和消息构造 |
| `WebBizException(HttpStatus status, String code, String msgPattern, Object... msgArgs)` | 使用 HTTP 状态码、自定义错误码和消息模板构造 |
| `WebBizException(Throwable throwable)` | 使用异常栈构造，默认 HTTP 500，code 取 500 状态名 |
| `WebBizException(String code, Throwable throwable)` | 使用自定义错误码和异常栈构造，默认 HTTP 500 |
| `WebBizException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 使用自定义错误码、异常栈和消息模板构造，默认 HTTP 500 |
| `WebBizException(HttpStatus status, String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 全参数构造 |

## 方法

### type

`ExceptionType type()`

> 获取异常类型（继承自 BizException）

**返回**: `ExceptionType` — 固定返回 `ExceptionType.BIZ`

### status

`HttpStatus status()`

> 获取 HTTP 状态码

**返回**: `HttpStatus` — HTTP 状态码

## 示例

```java
// 指定 HTTP 状态码
throw new WebBizException(HttpStatus.BAD_REQUEST, "参数错误");

// 自定义错误码 + HTTP 状态码
throw new WebBizException(HttpStatus.NOT_FOUND, "USER_NOT_FOUND", "用户不存在");

// 消息模板
throw new WebBizException(HttpStatus.BAD_REQUEST, "参数 {0} 不能为空", "name");

// 包装原始异常
throw new WebBizException("DB_ERROR", throwable);

// 将 BizException 重新包装为 WebBizException
WebBizException wrapped = WebBizException.of(bizEx, HttpStatus.BAD_REQUEST);
throw wrapped;
```