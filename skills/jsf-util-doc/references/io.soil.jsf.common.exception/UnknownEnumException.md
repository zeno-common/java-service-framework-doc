# UnknownEnumException

> 未知枚举类型异常，当根据状态值无法匹配到对应枚举时抛出

- **包**: io.soil.jsf.common.exception
- **父类**: `BaseException`

## 构造

### UnknownEnumException

`UnknownEnumException(Object status, Class<? extends Enum> enumClazz)`

> 构造未知枚举异常

**参数**:
- `status` (`Object`) — 无法匹配的状态值
- `enumClazz` (`Class<? extends Enum>`) — 枚举类对象

**消息模板**: `"未知的 {0} 枚举状态:{1}"` — {0}=枚举类名, {1}=状态值

## 方法

### module

`String module()`

> 获取异常模块名称

**返回**: `String` — 固定返回 `"JSF"`

## 示例

```java
// 在枚举的 of() 方法中使用
public Status of(int status) {
    for (Status e : values()) {
        if (e.status == status) return e;
    }
    throw new UnknownEnumException(status, Status.class);
}
```