# ExceptionType

> 异常类型枚举，用于标识异常的来源分类，对应 COLA 5 分层架构中的异常分类规则

- **包**: io.soil.jsf.common.exception
- **类型**: enum

## 枚举值

| 值 | 说明 |
|----|------|
| `UNKNOWN` | 未知异常，用于表示未分类的异常类型 |
| `BIZ` | 业务异常，Domain/App 层违反业务规则时抛出 |
| `SYS` | 系统异常，Infrastructure 层捕获技术异常后包装抛出 |
| `CLIENT` | 移动端导致的异常，比如 Adapter 层入参校验失败时抛出 |

## 示例

```java
// 在 BaseException 子类中实现 type() 方法
public class OrderException extends BaseException {
    @Override
    public ExceptionType type() { return ExceptionType.BIZ; }
}

// 在全局异常处理器中根据类型分类处理
if (ex.type() == ExceptionType.BIZ) {
    // 业务异常处理
} else if (ex.type() == ExceptionType.SYS) {
    // 系统异常处理
}
```
