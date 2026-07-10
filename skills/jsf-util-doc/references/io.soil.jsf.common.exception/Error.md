# Error

> 错误定义接口，用于以类型安全的方式定义错误码与错误描述

- **包**: io.soil.jsf.common.exception
- **类型**: interface

## 设计要点

1. **类型安全**：实现此接口的枚举类可作为 `BizException.of()`、`SysException.of()`、`ParamException.of()` 等静态工厂方法的参数，避免在业务代码中硬编码错误码和描述字符串
2. **code()**：返回错误码，格式建议为 `[业务]-[编码]`，例如 `ORDER-NOT-FOUND`
3. **desc()**：返回错误描述，支持 `MessageFormat` 模板语法，使用 `{0}`、`{1}` 等占位符进行参数替换

## 方法

### code

`String code()`

> 获取错误码

**返回**: `String` — 错误码

### desc

`String desc()`

> 获取错误描述（支持 MessageFormat 模板语法）

**返回**: `String` — 错误描述

## 示例

```java
// 定义领域错误码枚举
public enum OrderError implements Error {
    NOT_FOUND("ORDER-NOT-FOUND", "订单 {0} 不存在"),
    EXISTED("ORDER-EXISTED", "订单已存在");

    private final String code;
    private final String desc;
    OrderError(String code, String desc) { this.code = code; this.desc = desc; }
    @Override public String code() { return code; }
    @Override public String desc() { return desc; }
}

// 配合 BizException.of() 使用
throw BizException.of(OrderError.NOT_FOUND, orderId);

// 配合 SysException.of() 使用（带原始异常）
throw SysException.of(cause, OrderError.NOT_FOUND, orderId);
```