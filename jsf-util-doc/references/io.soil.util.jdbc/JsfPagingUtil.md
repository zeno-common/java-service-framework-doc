# JsfPagingUtil

> JSF 分页工具类，基于 REST API 规约的 URL 参数进行 PageHelper 分页处理

- **包**: io.soil.util.jdbc
- **依赖**: PageHelper

## 方法

### pageByUrlParam

`static <T> Page<T> pageByUrlParam()`

> 根据 URL 参数分页（默认查询总数）

**返回**: `Page<T>` — PageHelper 的 Page 对象

### pageByUrlParam (order)

`static <T> Page<T> pageByUrlParam(String order)`

> 根据 URL 参数分页，指定排序字段

**参数**:
- `order` (`String`) — 排序字段

**返回**: `Page<T>` — Page 对象

### pageByUrlParam (count)

`static <T> Page<T> pageByUrlParam(Boolean count)`

> 根据 URL 参数分页，指定是否查询总数

**参数**:
- `count` (`Boolean`) — 是否查询总数

**返回**: `Page<T>` — Page 对象

### pageByUrlParam (order, count)

`static <T> Page<T> pageByUrlParam(String order, boolean count)`

> 根据 URL 参数分页，优先 offset/limit，其次 pageNo/pageSize

**参数**:
- `order` (`String`) — 排序字段，null 时从 URL 参数获取
- `count` (`boolean`) — 是否查询总数

**返回**: `Page<T>` — Page 对象

### pageByUrlParam (pageNo, pageSize, order)

`static <T> Page<T> pageByUrlParam(Integer pageNo, Integer pageSize, String order)`

> 指定页码、每页条数和排序分页（默认查询总数）

**返回**: `Page<T>` — Page 对象

### pageByUrlParam (pageNo, pageSize, order, count)

`static <T> Page<T> pageByUrlParam(Integer pageNo, Integer pageSize, String order, boolean count)`

> 完整参数分页

**返回**: `Page<T>` — Page 对象

### offsetByUrlParams (offset, limit, order)

`static <T> Page<T> offsetByUrlParams(Integer offset, Integer limit, String order)`

> 使用偏移量分页（默认查询总数）

**返回**: `Page<T>` — Page 对象

### offsetByUrlParams (offset, limit, order, count)

`static <T> Page<T> offsetByUrlParams(Integer offset, Integer limit, String order, boolean count)`

> 使用偏移量分页

**返回**: `Page<T>` — Page 对象

## 示例

```java
// 最简用法：从 URL 参数自动获取分页信息
Page<User> page = JsfPagingUtil.pageByUrlParam();
List<User> users = userMapper.selectAll();

// 指定排序
Page<User> page = JsfPagingUtil.pageByUrlParam("name asc");

// 不查询总数（提升性能）
Page<User> page = JsfPagingUtil.pageByUrlParam(false);

// 偏移量分页
Page<User> page = JsfPagingUtil.offsetByUrlParams(0, 20, "id desc");
```