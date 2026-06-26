# CollectionUtil

> 集合工具类，提供集合转换、映射等常用操作

- **包**: io.soil.common.collection

## 方法

### toMap

`static <KEY,VALUE> Map<KEY,VALUE> toMap(Collection<VALUE> values, Function<VALUE,KEY> keyMapper)`

> 将集合转换为 Map，使用指定的 key 映射函数提取键

**参数**:
- `values` (`Collection<VALUE>`) — 源集合
- `keyMapper` (`Function<VALUE,KEY>`) — 键映射函数

**返回**: `Map<KEY,VALUE>` — 以 keyMapper 提取的键为键、原元素为值的 Map

### mapList

`static <T,R> List<R> mapList(Collection<T> source, Function<T,R> mapper)`

> 将源集合中的元素映射为新的列表

**参数**:
- `source` (`Collection<T>`) — 源集合
- `mapper` (`Function<T,R>`) — 映射函数

**返回**: `List<R>` — 映射后的新列表，源集合为空时返回空列表

### mapList (1 param)

`static <S,R,P> List<R> mapList(Collection<S> source, FunctionWithParam<S,R,P> mapper, P param1)`

> 使用带一个额外参数的映射函数映射为新的列表

**参数**:
- `source` (`Collection<S>`) — 源集合
- `mapper` (`FunctionWithParam<S,R,P>`) — 映射函数
- `param1` (`P`) — 额外参数

**返回**: `List<R>` — 映射后的新列表

### mapList (2 params)

`static <S,R,P1,P2> List<R> mapList(Collection<S> source, FunctionWith2Param<S,R,P1,P2> mapper, P1 p1, P2 p2)`

> 使用带两个额外参数的映射函数映射为新的列表

**参数**:
- `source` (`Collection<S>`) — 源集合
- `mapper` (`FunctionWith2Param<S,R,P1,P2>`) — 映射函数
- `p1` (`P1`) — 第一个额外参数
- `p2` (`P2`) — 第二个额外参数

**返回**: `List<R>` — 映射后的新列表

### mapList (3 params)

`static <S,R,P1,P2,P3> List<R> mapList(Collection<S> source, FunctionWith3Param<S,R,P1,P2,P3> mapper, P1 p1, P2 p2, P3 p3)`

> 使用带三个额外参数的映射函数映射为新的列表

**参数**:
- `source` (`Collection<S>`) — 源集合
- `mapper` (`FunctionWith3Param<S,R,P1,P2,P3>`) — 映射函数
- `p1` (`P1`) / `p2` (`P2`) / `p3` (`P3`) — 额外参数

**返回**: `List<R>` — 映射后的新列表

## 示例

```java
// 集合转 Map
Map<Long, User> userMap = CollectionUtil.toMap(users, User::getId);

// 简单映射
List<String> names = CollectionUtil.mapList(users, User::getName);

// 带额外参数映射
List<String> results = CollectionUtil.mapList(users,
    (user, prefix) -> prefix + user.getName(), "Hello ");
```