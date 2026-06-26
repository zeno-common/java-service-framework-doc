# `WafHttpExceptionResolver`

`package io.soil.waf.exception`

`@Slf4j` `@RestControllerAdvice`

WAF 全局异常处理器，自动捕获并处理 Web 层异常。

---

## Methods

### `ResponseEntity<WafHttpExceptionResponse> handleWebException(WafException e)`

`@ExceptionHandler(WafException.class)`

→ **ResponseEntity<WafHttpExceptionResponse>** — 处理 WAF 自定义异常

| Param | Type | Description |
|-------|------|-------------|
| `e` | `WafException` | WAF 异常对象 |

### `ResponseEntity<WafHttpExceptionResponse> handleWebException(Throwable throwable)`

`@ExceptionHandler(Throwable.class)`

→ **ResponseEntity<WafHttpExceptionResponse>** — 处理所有未捕获的异常

| Param | Type | Description |
|-------|------|-------------|
| `throwable` | `Throwable` | 原始异常对象 |