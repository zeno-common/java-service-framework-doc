# `ApplicationContextUtil`

`package io.soil.util.spring`

`@Component`

implements `ApplicationContextAware`

Spring ApplicationContext 工具类，提供在非 Spring 管理的类中获取 Bean 的能力。

- **Author:** zeno

---

## Methods

### `void setApplicationContext(ApplicationContext applicationContext)`

设置 Spring 应用上下文

| Param | Type | Description |
|-------|------|-------------|
| `applicationContext` | `ApplicationContext` | *(No description provided)* |

throws `BeansException` — 如果获取失败

---

### `static <T> T getBean(String name)`

→ **T** — 以所给名字注册的 Bean 实例

根据名称获取 Bean 实例

| Param | Type | Description |
|-------|------|-------------|
| `name` | `String` | Bean 的注册名称 |
| `<T>` | | Bean 的类型 |

throws `BeansException` — 如果获取失败

---

### `static <T> T getBean(Class<T> clazz)`

→ **T** — 对应类型的 Bean 实例

根据类型获取 Bean 实例

| Param | Type | Description |
|-------|------|-------------|
| `clazz` | `Class<T>` | Bean 的类型 |
| `<T>` | | Bean 的类型 |

throws `BeansException` — 如果获取失败