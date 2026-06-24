# BigNumSerializer

io.soil.waf.handler

extends NumberSerializer

@JacksonStdImpl

超出 JS 最大最小值处理

---

## Constants

| Name | Type | Value | Description |
|------|------|-------|-------------|
| MAX_SAFE_INTEGER | long | 9007199254740991L | 根据 JS Number.MAX_SAFE_INTEGER 与 Number.MIN_SAFE_INTEGER 得来 |
| MIN_SAFE_INTEGER | long | -9007199254740991L | 根据 JS Number.MAX_SAFE_INTEGER 与 Number.MIN_SAFE_INTEGER 得来 |
| INSTANCE | BigNumSerializer | 
ew BigNumSerializer(Number.class) | 提供实例 |

---

## Methods

### BigNumSerializer(Class<? extends Number> rawType)

→**BigNumSerializer** — *(No description provided)*

| Param | Type | Description |
|-------|------|-------------|
| awType | Class<? extends Number> | 数字类型 |

### oid serialize(Number value, JsonGenerator gen, SerializerProvider provider)

→**void** — *(No description provided)*

| Param | Type | Description |
|-------|------|-------------|
| alue | Number | 数字值 |
| gen | JsonGenerator | JSON 生成器 |
| provider | SerializerProvider | 序列化提供者 |
