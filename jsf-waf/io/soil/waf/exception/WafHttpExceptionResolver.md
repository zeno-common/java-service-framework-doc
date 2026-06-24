# WafHttpExceptionResolver

io.soil.waf.exception

@Slf4j @RestControllerAdvice

WAF 全局异常处理器，自动捕获并处理 Web 层异常。

使用 RestControllerAdvice 注解，自动注册为全局异常处理器。支持处理 WafException 和所有未捕获的 Throwable 异常，统一返回 WafHttpExceptionResponse 格式的 JSON 响应。

---

## Methods

### ResponseEntity<WafHttpExceptionResponse> handleWebException(WafException e)

@ExceptionHandler(WafException.class)

→**ResponseEntity<WafHttpExceptionResponse>** — 包含异常信息的 HTTP 响应，状态码由异常对象决定

处理 WAF 自定义异常

| Param | Type | Description |
|-------|------|-------------|
| e | WafException | WAF 异常对象 |

### ResponseEntity<WafHttpExceptionResponse> handleWebException(Throwable throwable)

@ExceptionHandler(Throwable.class)

→**ResponseEntity<WafHttpExceptionResponse>** — 包含异常信息的 HTTP 响应，状态码固定为 500

处理所有未捕获的异常

| Param | Type | Description |
|-------|------|-------------|
| 	hrowable | Throwable | 原始异常对象 |
