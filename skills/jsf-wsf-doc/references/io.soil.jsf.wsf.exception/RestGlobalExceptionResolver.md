# RestGlobalExceptionResolver

> WSF 全局异常处理器，自动捕获并处理 Web 层异常

- **包**: io.soil.jsf.wsf.exception
- **注解**: `@RestControllerAdvice`

## 方法

### handleValidationException (ParamException)

`ResponseEntity<RestExceptionResponse> handleValidationException(ParamException e)`

> 处理参数校验异常（在 Adapter 层主动抛出 `ParamException` 时触发）

**参数**:
- `e` (`ParamException` — 来自 `io.soil.jsf.common.exception` 包) — 参数校验异常对象

**返回**: `ResponseEntity<RestExceptionResponse>` — 包含异常信息的 HTTP 响应，状态码固定为 400

**默认值**: `errType` = `ExceptionType.PARAM`, `errCode` = `e.code()`, `errDesc` = `e.getMessage()`

### handleValidationException (MethodArgumentNotValidException)

`ResponseEntity<RestExceptionResponse> handleValidationException(MethodArgumentNotValidException e)`

> 处理参数校验异常（@Valid / @Validated 校验失败时抛出）

**参数**:
- `e` (`MethodArgumentNotValidException`) — 参数校验异常对象

**返回**: `ResponseEntity<RestExceptionResponse>` — 包含字段级错误信息的 HTTP 响应，状态码固定为 400

**默认值**: `errType` = `ExceptionType.PARAM`, `errCode` = `HttpStatus.BAD_REQUEST.name()`, `errDesc` = 字段错误消息（分号分隔）

### handleBaseException (WebBizException)

`ResponseEntity<RestExceptionResponse> handleBaseException(WebBizException e)`

> 处理 Web 业务自定义异常（如数据冲突等，在 Service 层进行业务校验时抛出）

**参数**:
- `e` (`WebBizException`) — Web 业务异常对象

**返回**: `ResponseEntity<RestExceptionResponse>` — 包含异常信息的 HTTP 响应，状态码由异常对象决定

### handleBaseException (BaseException)

`ResponseEntity<RestExceptionResponse> handleBaseException(BaseException e)`

> 处理 BaseException 自定义异常

**参数**:
- `e` (`BaseException`) — 自定义异常对象

**返回**: `ResponseEntity<RestExceptionResponse>` — 包含异常信息的 HTTP 响应，状态码固定为 500

### handleBaseException (Throwable)

`ResponseEntity<RestExceptionResponse> handleBaseException(Throwable throwable)`

> 处理所有未捕获的异常

**参数**:
- `throwable` (`Throwable`) — 原始异常对象

**返回**: `ResponseEntity<RestExceptionResponse>` — 包含异常信息的 HTTP 响应，状态码固定为 500

## 示例

```java
// RestGlobalExceptionResolver 通过 @RestControllerAdvice 自动注册
// 抛出 ParamException 时，自动返回 HTTP 400 + RestExceptionResponse
// errType = PARAM, errCode = 异常自定义码, errDesc = 异常消息

// 抛出 WebBizException 时，自动返回 RestExceptionResponse 格式 JSON
// 状态码由 WebBizException.status() 决定

// @Valid / @Validated 校验失败时，自动返回 HTTP 400 + RestExceptionResponse
// errType = PARAM, errDesc = 字段错误消息

// 抛出其他未捕获异常时，自动返回 HTTP 500 + RestExceptionResponse
```