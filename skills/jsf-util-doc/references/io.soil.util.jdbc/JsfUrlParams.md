# JsfUrlParams

> JSF URL 参数工具类，从 HTTP 请求中提取分页、排序、偏移等 URL 参数

- **包**: io.soil.util.jdbc

## 默认值

| 参数 | 默认值 | 最大值 |
|------|--------|--------|
| pageSize | 10 | 500 |
| pageNo | 1 | — |
| offset | 0 | — |
| limit | 10 | — |

## 方法

### offset

`static Integer offset(Integer defaultOffset)` / `static Integer offset()`

> 获取请求中的偏移量

**返回**: `Integer` — 偏移量，默认 0

### limit

`static Integer limit(Integer defaultLimit)` / `static Integer limit()`

> 获取请求中的限制条数

**返回**: `Integer` — 限制条数，默认 10

### pageSize

`static Integer pageSize(Integer defaultSize)` / `static Integer pageSize()`

> 获取请求中的每页条数，超过 500 自动截断

**返回**: `Integer` — 每页条数

### pageNo

`static Integer pageNo(Integer defaultPageNo)` / `static Integer pageNo()`

> 获取请求中的当前页码

**返回**: `Integer` — 当前页码，默认 1

### order

`static String order()`

> 获取请求中的排序参数

**返回**: `String` — 排序字符串，参数不存在时返回 null

### getOffsetId

`static Long getOffsetId()`

> 获取请求中的偏移 ID，用于轮询查询

**返回**: `Long` — 偏移 ID，参数不存在时返回 null

### getOffsetTime

`static String getOffsetTime()`

> 获取请求中的偏移时间，用于轮询查询

**返回**: `String` — 偏移时间字符串，参数不存在时返回 null

### getInteger

`static Integer getInteger(String paramName, Integer defaultValue)`

> 获取请求中指定参数名的整数值

**参数**:
- `paramName` (`String`) — 参数名
- `defaultValue` (`Integer`) — 默认值

**返回**: `Integer` — 参数值的整数形式

### getString

`static String getString(String paramName)`

> 获取请求中指定参数名的字符串值

**参数**:
- `paramName` (`String`) — 参数名

**返回**: `String` — 参数值字符串

## 示例

```java
// 在 Controller 中直接使用
Integer pageNo = JsfUrlParams.pageNo();       // 从 URL 获取 $pageNo，默认 1
Integer pageSize = JsfUrlParams.pageSize();   // 从 URL 获取 $pageSize，默认 10
String order = JsfUrlParams.order();          // 从 URL 获取 $order

// 带默认值
Integer offset = JsfUrlParams.offset(100);    // 默认 100
```