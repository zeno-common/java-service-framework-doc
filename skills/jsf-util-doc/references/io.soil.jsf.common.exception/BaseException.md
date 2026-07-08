# BaseException

> 业务异常基类，所有业务、系统、其他级异常的统一抽象父类

- **包**: io.soil.jsf.common.exception
- **父类**: `RuntimeException`
- **Lombok**: `@Slf4j`
- **抽象类** — 子类必须实现 `type()` 方法

## 设计要点

1. **异常规约**：每个业务从本类派生并实现 `type()` 方法，返回异常类型（`ExceptionType` 枚举），以便在日志和监控中快速定位异常来源
2. **异常状态码**：通过 `code()` 返回异常状态码，格式建议为 `[业务]-[编码]`，例如 `ORDER-EXSITED`、`DB-SAVE-FAILED`
3. **消息格式化**：异常消息支持 `MessageFormat` 模板语法，使用 `{0}`、`{1}` 等占位符进行参数替换
4. **异常栈输出**：`getStackTraceString()` 方法仅在 DEBUG 日志级别下返回完整异常栈，非 DEBUG 级别返回空字符串，避免生产环境输出冗余信息

## 构造

| 签名 | 说明 |
|------|------|
| `BaseException(String msg)` | 使用消息构造 |
| `BaseException(String msgPattern, Object... msgArgs)` | 使用消息模板构造（MessageFormat 格式化） |
| `BaseException(Throwable throwable)` | 使用异常栈构造，消息取 throwable.getMessage() |
| `BaseException(Throwable throwable, String msg)` | 使用异常栈和消息构造 |
| `BaseException(Throwable throwable, String msgPattern, Object... msgArgs)` | 使用异常栈和消息模板构造 |
| `BaseException(String code, Throwable throwable)` | 使用异常状态码和异常栈构造，消息取 throwable.getMessage() |
| `BaseException(String code, Throwable throwable, String msg)` | 使用异常状态码、异常栈和消息构造 |
| `BaseException(String code, Throwable throwable, String msgPattern, Object... msgArgs)` | 全参数构造 |

## 方法

### type

`abstract ExceptionType type()`

> 获取异常类型，类型可以是业务类型、系统类型、其他类型等

**返回**: `ExceptionType` — 异常类型枚举

### code

`String code()`

> 获取异常状态码

**返回**: `String` — 异常状态码

### getStackTraceString

`String getStackTraceString()`

> 获取当前异常的栈字符串

**返回**: `String` — 异常栈字符串（非 debug 模式返回空字符串）

### getStackTraceString (static)

`static String getStackTraceString(Throwable throwable)`

> 获取指定异常的栈字符串

**参数**:
- `throwable` (`Throwable`) — 异常对象

**返回**: `String` — 异常栈字符串（非 debug 模式返回空字符串）

## 示例

```java
public class MyException extends BaseException {
    @Override
    public ExceptionType type() { return ExceptionType.BIZ; }

    public MyException(String msg) { super(msg); }
    public MyException(String pattern, Object... args) { super(pattern, args); }
}

// 使用消息模板
throw new MyException("用户 {0} 不存在", userId);

// 包装原始异常
throw new MyException(cause, "操作失败");
```