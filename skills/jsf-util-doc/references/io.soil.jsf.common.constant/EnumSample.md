# EnumSample

> 枚举定义参考示例，展示 JSF 枚举的标准定义模式

- **包**: io.soil.jsf.common.constant
- **类型**: enum

## 枚举值

| 值 | status |
|----|--------|
| `SAMPLE` | 0 |

## 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `status` | `int` | 枚举状态值 |

## 方法

### status

`int status()`

> 获取枚举状态值

**返回**: `int` — 枚举状态值

### of

`EnumSample of(int status)`

> 根据状态值获取枚举对象

**参数**:
- `status` (`int`) — 状态值

**返回**: `EnumSample` — 枚举对象

**异常**: `UnknownEnumException` — 无法匹配时抛出

## 示例

```java
// 定义枚举
public enum Status {
    ACTIVE(1), INACTIVE(0);

    private final int status;

    Status(int status) { this.status = status; }
    public int status() { return status; }
    public Status of(int status) {
        for (Status e : values()) {
            if (e.status == status) return e;
        }
        throw new UnknownEnumException(status, Status.class);
    }
}
```