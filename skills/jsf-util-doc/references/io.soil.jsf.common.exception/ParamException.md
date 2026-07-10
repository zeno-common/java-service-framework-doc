# ParamException

> 参数校验异常，用于表示请求入参不合法（如非空、格式校验失败等），由 Adapter 层在参数校验时抛出

- **包**: io.soil.jsf.common.exception
- **父类**: `BaseException`
- **修饰**: `final`
- **异常类型**: `ExceptionType.PARAM`

## 说明

`ParamException` 继承自 `BaseException`，`type()` 固定返回 `ExceptionType.PARAM`。当它在 COLA 5 分层架构的 Adapter 层被抛出后，由 Web 层的全局异常处理器统一捕获，转换为标准错误响应（`errType = PARAM`，`errCode = 异常自定义码`，`errDesc = 异常消息`）。

推荐通过 `of(Error, Object...)` 静态工厂方法创建实例，配合实现 `Error` 接口的枚举使用。

## 静态方法

### of

`static ParamException of(Error error, Object... descArgs)`

> 根据错误定义和描述参数构造参数校验异常（无原始原因）

**参数**:
- `error` (`Error`) — 错误定义（提供 code 和 desc 模板）
- `descArgs` (`Object...`) — 描述模板参数（MessageFormat 格式化）

**返回**: `ParamException` — 参数校验异常实例

### of (with cause)

`static ParamException of(Throwable cause, Error error, Object... descArgs)`

> 根据错误定义、原始原因和描述参数构造参数校验异常

**参数**:
- `cause` (`Throwable`) — 原始异常原因
- `error` (`Error`) — 错误定义（提供 code 和 desc 模板）
- `descArgs` (`Object...`) — 描述模板参数（MessageFormat 格式化）

**返回**: `ParamException` — 参数校验异常实例

## 构造

| 签名 | 说明 |
|------|------|
| `ParamException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 全参数构造（private） |

## 方法

### type

`ExceptionType type()`

> 获取异常类型

**返回**: `ExceptionType` — 固定返回 `ExceptionType.PARAM`

## 示例

```java
// 定义参数错误码枚举
public enum ParamError implements Error {
    INVALID("PARAM-INVALID", "参数 {0} 不合法"),
    NOT_NULL("PARAM-NOT-NULL", "参数 {0} 不能为空");

    private final String code;
    private final String desc;
    ParamError(String code, String desc) { this.code = code; this.desc = desc; }
    @Override public String code() { return code; }
    @Override public String desc() { return desc; }
}

// 通过 Error 枚举构造（推荐）
throw ParamException.of(ParamError.NOT_NULL, "name");

// 带原始异常
throw ParamException.of(cause, ParamError.INVALID, "age");
```