# RestExceptionResponse

> WSF 全局统一异常处理，用于封装异常信息返回给客户端

- **包**: io.soil.jsf.wsf.exception
- **Lombok**: `@Data` — 所有字段均有 getter/setter [Lombok 生成]

## 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `errType` | `ExceptionType` | 异常类型 |
| `errCode` | `String` | 异常状态码 |
| `errDesc` | `String` | 异常消息 |
| `trace` | `String` | 异常栈信息 |

## 方法

### createFrom (Throwable)

`static RestExceptionResponse createFrom(Throwable ex)`

> 根据异常对象创建异常响应 VO

**参数**:
- `ex` (`Throwable`) — 异常对象

**返回**: `RestExceptionResponse` — 异常响应 VO

**默认值**: `errType` = `ExceptionType.SYS`, `errCode` = `HttpStatus.INTERNAL_SERVER_ERROR.name()`, `errDesc` = `ex.getMessage()`

### createFrom (WebBizException)

`static RestExceptionResponse createFrom(WebBizException ex)`

> 根据异常对象创建异常响应 VO

**参数**:
- `ex` (`WebBizException`) — WSF 异常对象

**返回**: `RestExceptionResponse` — 异常响应 VO

**默认值**: `errType` = `ex.type()`, `errCode` = `HttpStatus.INTERNAL_SERVER_ERROR.name()`, `errDesc` = `ex.getMessage()`

### createFrom (BaseException)

`static RestExceptionResponse createFrom(BaseException ex)`

> 根据异常对象创建异常响应 VO

**参数**:
- `ex` (`BaseException`) — 异常对象

**返回**: `RestExceptionResponse` — 异常响应 VO

**默认值**: `errType` = `ex.type()`, `errCode` = `ex.code()`, `errDesc` = `ex.getMessage()`

## 示例

```java
RestExceptionResponse response = RestExceptionResponse.createFrom(exception);
// response.getErrType()  -> ExceptionType.SYS
// response.getErrCode()  -> "INTERNAL_SERVER_ERROR"
// response.getErrDesc()  -> exception.getMessage()
// response.getTrace()    -> 堆栈字符串
```
