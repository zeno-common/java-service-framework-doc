# WebBizException

> Web 业务异常，可指定 HTTP 状态码的业务异常，用于支持 REST API 异常响应场景。继承 BizException，在业务异常基础上额外持有 HTTP 状态码，由全局异常处理器按异常对象自带的状态码返回对应的 HTTP 响应

- **包**: io.soil.jsf.wsf.exception
- **父类**: `BizException`（io.soil.jsf.common.exception）
- **修饰**: `final`
- **异常类型**: `ExceptionType.BIZ`

## 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `status` | `HttpStatus` | HTTP 状态码 |

## 静态方法

### of

`static WebBizException of(HttpStatus status, BizException e)`

> 将业务异常重新包装为 WebBizException 对象，保留原始异常码和消息，同时指定 HTTP 状态码

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
// 指定 HTTP 状态码 + 自定义错误码 + 消息
throw new WebBizException(HttpStatus.BAD_REQUEST, "PARAM_ERROR", "参数错误");

// 自定义错误码 + HTTP 状态码
throw new WebBizException(HttpStatus.NOT_FOUND, "USER_NOT_FOUND", "用户不存在");

// 消息模板
throw new WebBizException(HttpStatus.BAD_REQUEST, "PARAM_INVALID", "参数 {0} 不能为空", "name");

// 包装原始异常
throw new WebBizException(HttpStatus.INTERNAL_SERVER_ERROR, "DB_ERROR", throwable);

// 自定义错误码 + 异常栈 + 消息
throw new WebBizException(HttpStatus.INTERNAL_SERVER_ERROR, "DB_SAVE_FAILED", throwable, "数据库保存失败");

// 将 BizException 重新包装为 WebBizException
WebBizException wrapped = WebBizException.of(HttpStatus.BAD_REQUEST, bizEx);
throw wrapped;
```