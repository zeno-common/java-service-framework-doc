# WafHttpExceptionResponse

io.soil.waf.exception

@Data

WAF 异常响应内容，用于封装异常信息返回给客户端。

---

## Fields

| Name | Type | Description |
|------|------|-------------|
| module | String | 异常模块名称 |
| errCode | String | 异常状态码 |
| errDesc | String | 异常消息 |
| 	race | String | 异常栈信息 |

---

## Methods

### static WafHttpExceptionResponse createFrom(Throwable ex)

→**WafHttpExceptionResponse** — 根据异常对象创建异常响应 VO

| Param | Type | Description |
|-------|------|-------------|
| ex | Throwable | 异常对象
