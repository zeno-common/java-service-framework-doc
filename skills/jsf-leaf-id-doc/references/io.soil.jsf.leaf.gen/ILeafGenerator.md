# ILeafGenerator

> 工作节点协调器接口，提供 dataCenterId 和 workerId 的获取能力

- **包**: io.soil.jsf.leaf.gen
- **类型**: 接口

## 说明

`ILeafGenerator` 是工作节点协调器的顶层接口，定义了获取数据中心 ID 和工作节点 ID 的方法。框架提供两种实现：
- `LeafDefaultGenerator` — 静态配置模式
- `LeafJdbcGenerator` — JDBC 数据库协调模式

由 `LeafAutoConfig` 根据配置自动注册对应的实现 Bean。

## 方法

### dataCenterId

`int dataCenterId()`

> 获取数据中心 ID

**返回**: `int` — 数据中心 ID，范围 0 ~ 31

### workerId

`int workerId()`

> 获取工作节点 ID

**返回**: `int` — 工作节点 ID，范围 0 ~ 255