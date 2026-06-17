# `UnknownEnumException`

`package io.soil.common.exception`

extends `BaseException`

未知的枚举类型异常，当根据状态值无法匹配到对应的枚举时抛出。

- **Author:** zeno.w

---

## Constructors

### `UnknownEnumException(Object status, Class<? extends Enum> enumClazz)`

构造未知枚举异常

| Param | Type | Description |
|-------|------|-------------|
| `status` | `Object` | 无法匹配的状态值 |
| `enumClazz` | `Class<? extends Enum>` | 枚举类对象 |

---

## Methods

### `protected String module()`

→ **String** — 模块名

获取异常模块名称