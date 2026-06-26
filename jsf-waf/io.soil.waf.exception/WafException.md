# `WafException`

`package io.soil.waf.exception`

extends `BaseException`

WAF 异常类，用于 Web 应用框架层的异常处理。

---

## Methods

### `WafException(HttpStatus status, String msg)`

使用 HTTP 状态码和消息构造 WAF 异常

| Param | Type | Description |
|-------|------|-------------|
| `status` | `HttpStatus` | HTTP 状态码 |
| `msg` | `String` | 异常消息 |

### `WafException(HttpStatus status, String msgPattern, Object... msgArgs)`

使用 HTTP 状态码和消息模板构造 WAF 异常

| Param | Type | Description |
|-------|------|-------------|
| `status` | `HttpStatus` | HTTP 状态码 |
| `msgPattern` | `String` | java.text.MessageFormat 消息模板 |
| `msgArgs` | `Object...` | 消息模板参数 |

### `WafException(String code, HttpStatus status, String msg)`

使用自定义异常状态码和 HTTP 状态码构造 WAF 异常

| Param | Type | Description |
|-------|------|-------------|
| `code` | `String` | 自定义异常状态码 |
| `status` | `HttpStatus` | HTTP 状态码 |
| `msg` | `String` | 异常消息 |

### `WafException(String code, HttpStatus status, String msgPattern, Object... msgArgs)`

使用自定义异常状态码、HTTP 状态码和消息模板构造 WAF 异常

| Param | Type | Description |
|-------|------|-------------|
| `code` | `String` | 自定义异常状态码 |
| `status` | `HttpStatus` | HTTP 状态码 |
| `msgPattern` | `String` | java.text.MessageFormat 消息模板 |
| `msgArgs` | `Object...` | 消息模板参数 |

### `WafException(Throwable throwable)`

使用异常栈构造 WAF 异常，默认 HTTP 状态码 500

| Param | Type | Description |
|-------|------|-------------|
| `throwable` | `Throwable` | 原始异常 |

### `WafException(String code, Throwable throwable)`

使用自定义异常状态码和异常栈构造 WAF 异常

| Param | Type | Description |
|-------|------|-------------|
| `code` | `String` | 自定义异常状态码 |
| `throwable` | `Throwable` | 原始异常 |

### `WafException(String code, Throwable throwable, String msgPattern, Object... msgArgs)`

使用自定义异常状态码、异常栈和消息模板构造 WAF 异常

| Param | Type | Description |
|-------|------|-------------|
| `code` | `String` | 自定义异常状态码 |
| `throwable` | `Throwable` | 原始异常 |
| `msgPattern` | `String` | java.text.MessageFormat 消息模板 |
| `msgArgs` | `Object...` | 消息模板参数 |

### `WafException(String code, HttpStatus status, Throwable throwable, String msgPattern, Object... msgArgs)`

全参数构造 WAF 异常

| Param | Type | Description |
|-------|------|-------------|
| `code` | `String` | 自定义异常状态码 |
| `status` | `HttpStatus` | HTTP 状态码 |
| `throwable` | `Throwable` | 原始异常 |
| `msgPattern` | `String` | java.text.MessageFormat 消息模板 |
| `msgArgs` | `Object...` | 消息模板参数 |

### `String module()`

→ **String** — 获取异常所属模块名称

### `HttpStatus status()`

→ **HttpStatus** — 获取 HTTP 状态码

### `String code()`

→ **String** — 获取自定义异常状态码