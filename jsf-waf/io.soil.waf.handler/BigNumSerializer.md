# `BigNumSerializer`

`package io.soil.waf.handler`

extends `NumberSerializer`

`@JacksonStdImpl`

超出 JS 最大最小值处理

---

## Constants

| Name | Type | Value | Description |
|------|------|-------|-------------|
| `INSTANCE` | `BigNumSerializer` | `new BigNumSerializer(Number.class)` | 提供实例 |

---

## Methods

### `BigNumSerializer(Class<? extends Number> rawType)`

构造 BigNumSerializer

| Param | Type | Description |
|-------|------|-------------|
| `rawType` | `Class<? extends Number>` | 数字类型 |

### `void serialize(Number value, JsonGenerator gen, SerializerProvider provider)`

序列化数字为字符串，防止 JS 精度丢失

| Param | Type | Description |
|-------|------|-------------|
| `value` | `Number` | 数字值 |
| `gen` | `JsonGenerator` | JSON 生成器 |
| `provider` | `SerializerProvider` | 序列化提供者 |