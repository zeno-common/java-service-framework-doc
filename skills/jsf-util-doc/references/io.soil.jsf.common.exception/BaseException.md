# BaseException

> 异常基类，提供消息模板格式化和异常栈字符串获取能力

- **包**: io.soil.jsf.common.exception
- **父类**: `RuntimeException`
- **Lombok**: `@Slf4j`
- **抽象类** — 子类必须实现 `module()` 方法

## 构造

| 签名 | 说明 |
|------|------|
| `BaseException(String msg)` | 使用消息构造 |
| `BaseException(String msgPattern, Object... msgArgs)` | 使用消息模板构造（MessageFormat 格式化） |
| `BaseException(Throwable throwable, String msg)` | 使用异常栈和消息构造 |
| `BaseException(Throwable throwable)` | 使用异常栈构造，消息取 throwable.getMessage() |
| `BaseException(Throwable throwable, String msgPattern, Object... msgArgs)` | 全参数构造 |

## 方法

### module

`abstract String module()`

> 获取异常模块名称，子类必须实现

**返回**: `String` — 模块名

### getStackTraceString

`String getStackTraceString()`

> 获取当前异常的栈字符串

**返回**: `String` — 异常栈字符串（非 debug 模式返回空字符串）

### getStackTraceString

`static String getStackTraceString(Throwable throwable)`

> 获取指定异常的栈字符串

**参数**:
- `throwable` (`Throwable`) — 异常对象

**返回**: `String` — 异常栈字符串（非 debug 模式返回空字符串）

## 示例

```java
public class MyException extends BaseException {
    @Override
    protected String module() { return "MY-MODULE"; }

    public MyException(String msg) { super(msg); }
    public MyException(String pattern, Object... args) { super(pattern, args); }
}

// 使用消息模板
throw new MyException("用户 {0} 不存在", userId);

// 包装原始异常
throw new MyException(cause, "操作失败");
```