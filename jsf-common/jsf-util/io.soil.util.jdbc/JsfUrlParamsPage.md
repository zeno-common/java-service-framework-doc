# `JsfUrlParamsPage`

`package io.soil.util.jdbc`

extends `com.mybatisflex.core.paginate.Page<T>`

基于 URL 参数的 MyBatis-Flex 分页对象，继承 Page。

从 HTTP 请求的 URL 参数中自动提取分页信息（页码、每页条数），支持 pageNo/pageSize 和 offset/limit 两种分页模式。排序参数通过 JsfUrlParams.order() 获取，由调用方应用于 QueryWrapper。

- **Type Parameters:** `<T>` — 分页数据类型
- **Author:** koala

---

## Constructors

### `JsfUrlParamsPage()`

无参构造函数。

---

### `JsfUrlParamsPage(int pageNumber, int pageSize)`

分页构造函数

| Param | Type | Description |
|-------|------|-------------|
| `pageNumber` | `int` | 当前页 |
| `pageSize` | `int` | 每页显示条数 |

---

### `JsfUrlParamsPage(int pageNumber, int pageSize, long totalRow)`

分页构造函数

| Param | Type | Description |
|-------|------|-------------|
| `pageNumber` | `int` | 当前页 |
| `pageSize` | `int` | 每页显示条数 |
| `totalRow` | `long` | 总数 |

---

## Methods

### `boolean hasPrevious()`

→ **boolean** — true / false

是否存在上一页

---

### `boolean hasNext()`

→ **boolean** — true / false

是否存在下一页

---

### `String order()`

→ **String** — 排序字符串，参数不存在时返回 null

获取请求中的排序参数

---

### `static <T> JsfUrlParamsPage<T> of(long pageNumber, long pageSize)`

→ **JsfUrlParamsPage\<T\>** — 分页对象

创建分页对象，指定当前页和每页条数

| Param | Type | Description |
|-------|------|-------------|
| `pageNumber` | `long` | 当前页 |
| `pageSize` | `long` | 每页显示条数 |
| `<T>` | | 分页数据类型 |

---

### `static <T> JsfUrlParamsPage<T> of(long pageNumber, long pageSize, long totalRow)`

→ **JsfUrlParamsPage\<T\>** — 分页对象

创建分页对象，指定当前页、每页条数和总数

| Param | Type | Description |
|-------|------|-------------|
| `pageNumber` | `long` | 当前页 |
| `pageSize` | `long` | 每页显示条数 |
| `totalRow` | `long` | 总数 |
| `<T>` | | 分页数据类型 |

---

### `static <T> JsfUrlParamsPage<T> ofUrlParams()`

→ **JsfUrlParamsPage\<T\>** — 分页对象

从 URL 参数创建分页对象（默认查询总数）

| Param | Type | Description |
|-------|------|-------------|
| `<T>` | | 分页数据类型 |