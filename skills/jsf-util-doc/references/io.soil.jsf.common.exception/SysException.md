# SysException

> 系统异常，用于表示基础设施层捕获并包装的技术异常（如数据库访问失败、外部服务调用异常），由 Infrastructure 层抛出

- **包**: io.soil.jsf.common.exception
- **父类**: `BaseException`
- **修饰**: `final`
- **异常类型**: `ExceptionType.SYS`

## 说明

`SysException` 继承自 `BaseException`，`type()` 固定返回 `ExceptionType.SYS`。当它在 COLA 5 分层架构的 Infrastructure 层将底层技术异常包装后抛出，由 Web 层的全局异常处理器统一捕获，转换为标准错误响应（`errType = SYS`，`errCode = 异常自定义码`，`errDesc = 异常消息`），且不向前端暴露底层技术细节。

推荐通过 `of(Error, Object...)` 静态工厂方法创建实例，配合实现 `Error` 接口的枚举使用。

## 静态方法

### of

`static SysException of(Error error, Object... descArgs)`

> 根据错误定义和描述参数构造系统异常（无原始原因）

**参数**:
- `error` (`Error`) — 错误定义（提供 code 和 desc 模板）
- `descArgs` (`Object...`) — 描述模板参数（MessageFormat 格式化）

**返回**: `SysException` — 系统异常实例

### of (with cause)

`static SysException of(Throwable cause, Error error, Object... descArgs)`

> 根据错误定义、原始原因和描述参数构造系统异常

**参数**:
- `cause` (`Throwable`) — 原始异常原因
- `error` (`Error`) — 错误定义（提供 code 和 desc 模板）
- `descArgs` (`Object...`) — 描述模板参数（MessageFormat 格式化）

**返回**: `SysException` — 系统异常实例

## 构造

| 签名 | 说明 |
|------|------|
| `SysException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 全参数构造（private） |

## 方法

### type

`ExceptionType type()`

> 获取异常类型

**返回**: `ExceptionType` — 固定返回 `ExceptionType.SYS`

## 示例

```java
// 定义基础设施错误码枚举
public enum DbError implements Error {
    SAVE_FAILED("DB-SAVE-FAILED", "数据库保存失败"),
    CONNECTION_ERROR("DB-CONN-ERROR", "数据库连接失败");

    private final String code;
    private final String desc;
    DbError(String code, String desc) { this.code = code; this.desc = desc; }
    @Override public String code() { return code; }
    @Override public String desc() { return desc; }
}

// 通过 Error 枚举构造（推荐）
throw SysException.of(DbError.SAVE_FAILED);

// 带原始异常
throw SysException.of(e, DbError.CONNECTION_ERROR);
```