# `WafHttpExceptionResponse`

`package io.soil.waf.exception`

`@Data`

WAF 异常响应内容，用于封装异常信息返回给客户端。

---

## Methods

### `static WafHttpExceptionResponse createFrom(Throwable ex)`

根据异常对象创建异常响应 VO

| Param | Type | Description |
|-------|------|-------------|
| `ex` | `Throwable` | 异常对象 |

→ **WafHttpExceptionResponse** — 异常响应 VO