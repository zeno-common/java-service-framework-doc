# ErrorDefine

> 错误定义接口，用于以枚举方式统一声明异常码与异常消息

- **包**: io.soil.jsf.common.exception
- **类型**: `interface`

## 说明

`ErrorDefine` 是一个函数式接口，实现此接口的枚举可直接作为 `BizException.of()`、`ParamException.of()`、`SysException.of()` 的参数，避免在业务代码中硬编码异常码和消息字符串。

消息支持 `MessageFormat` 模板语法，可在 `of()` 方法调用时传入模板参数。

## 方法

### code

`String code()`

> 获取异常码

**返回**: `String` — 异常码，建议格式为 `[业务]-[编码]`，例如 `ORDER-NOT-FOUND`

### msg

`String msg()`

> 获取异常消息，支持 `MessageFormat` 模板语法

**返回**: `String` — 异常消息模板

## 示例

```java
enum OrderError implements ErrorDefine {
    NOT_FOUND("ORDER-NOT-FOUND", "订单 {0} 不存在"),
    EXISTED("ORDER-EXISTED", "订单已存在");

    private final String code;
    private final String msg;

    OrderError(String code, String msg) { this.code = code; this.msg = msg; }
    public String code() { return code; }
    public String msg() { return msg; }
}

// 直接使用
throw BizException.of(OrderError.NOT_FOUND);

// 带消息模板参数
throw BizException.of(OrderError.NOT_FOUND, orderId);

// 带原始异常
throw SysException.of(cause, OrderError.NOT_FOUND);
```