# JsfUrlParamsPage

> 基于 URL 参数的 MyBatis-Flex 分页对象，继承 Page

- **包**: io.soil.jsf.util.jdbc
- **父类**: `Page<T>`（MyBatis-Flex）
- **泛型**: `<T>` 分页数据类型

## 构造

| 签名 | 说明 |
|------|------|
| `JsfUrlParamsPage()` | 默认构造 |
| `JsfUrlParamsPage(int pageNumber, int pageSize)` | 指定页码和每页条数 |
| `JsfUrlParamsPage(int pageNumber, int pageSize, long totalRow)` | 指定页码、每页条数和总数 |

## 方法

### hasPrevious

`boolean hasPrevious()`

> 是否存在上一页

**返回**: `boolean` — pageNumber > 1

### hasNext

`boolean hasNext()`

> 是否存在下一页

**返回**: `boolean` — pageNumber < totalPage

### order

`String order()`

> 获取请求中的排序参数

**返回**: `String` — 排序字符串，参数不存在时返回 null

### of (pageNumber, pageSize)

`static <T> JsfUrlParamsPage<T> of(long pageNumber, long pageSize)`

> 创建分页对象

**返回**: `JsfUrlParamsPage<T>`

### of (pageNumber, pageSize, totalRow)

`static <T> JsfUrlParamsPage<T> of(long pageNumber, long pageSize, long totalRow)`

> 创建分页对象（含总数）

**返回**: `JsfUrlParamsPage<T>`

### ofUrlParams

`static <T> JsfUrlParamsPage<T> ofUrlParams()`

> 从 URL 参数创建分页对象

**返回**: `JsfUrlParamsPage<T>` — 自动提取 $pageNo 和 $pageSize

## 示例

```java
// 从 URL 参数自动创建
JsfUrlParamsPage<User> page = JsfUrlParamsPage.ofUrlParams();

// 手动指定
JsfUrlParamsPage<User> page = JsfUrlParamsPage.of(1, 20);

// 含总数
JsfUrlParamsPage<User> page = JsfUrlParamsPage.of(1, 20, 100L);

// 排序由调用方应用于 QueryWrapper
String order = page.order();
```