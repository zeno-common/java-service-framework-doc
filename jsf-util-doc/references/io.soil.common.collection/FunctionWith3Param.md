# FunctionWith3Param

> 带三个额外参数的函数式接口

- **包**: io.soil.common.collection
- **注解**: `@FunctionalInterface`
- **泛型**: `<S>` 源类型, `<R>` 返回类型, `<P1>` / `<P2>` / `<P3>` 额外参数类型

## 方法

### apply

`R apply(S s, P1 p1, P2 p2, P3 p3)`

> 应用函数

**参数**:
- `s` (`S`) — 源对象
- `p1` (`P1`) / `p2` (`P2`) / `p3` (`P3`) — 额外参数

**返回**: `R` — 函数执行结果