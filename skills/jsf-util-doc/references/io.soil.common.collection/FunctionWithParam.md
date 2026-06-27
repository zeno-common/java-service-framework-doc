# FunctionWithParam

> 带一个额外参数的函数式接口，扩展标准 Function 以支持额外参数传递

- **包**: io.soil.common.collection
- **注解**: `@FunctionalInterface`
- **泛型**: `<S>` 源类型, `<R>` 返回类型, `<P>` 额外参数类型

## 方法

### apply

`R apply(S s, P p)`

> 应用函数

**参数**:
- `s` (`S`) — 源对象
- `p` (`P`) — 额外参数

**返回**: `R` — 函数执行结果