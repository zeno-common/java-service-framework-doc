# `BaseException`

`package io.soil.common.exception`

`@Slf4j`

extends `RuntimeException`

异常基类。

主要以下用途
1. 用于制定通用的异常信息，给派生类的构建函数定义进行参考。
2. 有助于构异异常类的构建，并提供多种场景下异常类构建函数的定义参考，方便快速定义异常类和易于实例化异常类对象。

- **Author:** zeno.w

---

## Constructors

### `protected BaseException(String msg)`

*(No description provided)*

| Param | Type | Description |
|-------|------|-------------|
| `msg` | `String` | *(No description provided)* |

---

### `protected BaseException(String msgPattern, Object... msgArgs)`

*(No description provided)*

| Param | Type | Description |
|-------|------|-------------|
| `msgPattern` | `String` | *(No description provided)* |
| `msgArgs` | `Object...` | *(No description provided)* |

---

### `protected BaseException(Throwable throwable, String msg)`

*(No description provided)*

| Param | Type | Description |
|-------|------|-------------|
| `throwable` | `Throwable` | *(No description provided)* |
| `msg` | `String` | *(No description provided)* |

---

### `protected BaseException(Throwable throwable)`

*(No description provided)*

| Param | Type | Description |
|-------|------|-------------|
| `throwable` | `Throwable` | *(No description provided)* |

---

### `protected BaseException(Throwable throwable, String msgPattern, Object... msgArgs)`

*(No description provided)*

| Param | Type | Description |
|-------|------|-------------|
| `throwable` | `Throwable` | *(No description provided)* |
| `msgPattern` | `String` | *(No description provided)* |
| `msgArgs` | `Object...` | *(No description provided)* |

---

## Methods

### `protected abstract String module()`

→ **String** — 模块名

获取异常模块名称

---

### `String getStackTraceString()`

→ **String** — 异常栈字符串

获取异常栈字符串

---

### `static String getStackTraceString(Throwable throwable)`

→ **String** — 异常栈字符串

获取异常栈字符串

| Param | Type | Description |
|-------|------|-------------|
| `throwable` | `Throwable` | *(No description provided)* |