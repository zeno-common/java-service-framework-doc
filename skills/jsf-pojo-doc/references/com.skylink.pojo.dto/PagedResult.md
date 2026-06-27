# PagedResult

> 分页结果响应体，封装分页查询的返回结果

- **包**: com.skylink.pojo.dto
- **泛型**: `<T>` 分页数据的元素类型
- **Lombok**: `@Data` — 所有字段均有 getter/setter [Lombok 生成]

## 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `total` | `int` | 查询总数 |
| `items` | `Collection<T>` | 返回项列表 |

## 构造

| 签名 | 说明 |
|------|------|
| `PagedResult()` | 默认构造，total=0, items=空列表 |
| `PagedResult(int total)` | 指定总数，items=空列表 |

## 静态方法

### empty

`static <T> PagedResult<T> empty()`

> 返回空结果，total=0, items=空列表

**返回**: `PagedResult<T>` — 空的分页结果

### empty

`static <T> PagedResult<T> empty(long total)`

> 返回空列表但指定总数的分页结果

**参数**:
- `total` (`long`) — 查询总数

**返回**: `PagedResult<T>` — 空列表但指定总数的分页结果

### of

`static <T> PagedResult<T> of(long total, Collection<T> items)`

> 根据总数和集合列表构建分页结果

**参数**:
- `total` (`long`) — 总数
- `items` (`Collection<T>`) — 分页列表，为 null 时自动替换为空列表

**返回**: `PagedResult<T>` — 分页结果对象

### of

`static <T> PagedResult<T> of(int total, Collection<T> items)`

> 根据总数和集合列表构建分页结果

**参数**:
- `total` (`int`) — 总数
- `items` (`Collection<T>`) — 分页列表，为 null 时自动替换为空列表

**返回**: `PagedResult<T>` — 分页结果对象

## 示例

```java
// 空结果
PagedResult<User> empty = PagedResult.empty();

// 指定总数但空列表
PagedResult<User> emptyWithTotal = PagedResult.empty(100L);

// 构建分页结果
PagedResult<User> result = PagedResult.of(100, userList);

// items 为 null 时自动替换为空列表
PagedResult<User> safe = PagedResult.of(0, null);
```