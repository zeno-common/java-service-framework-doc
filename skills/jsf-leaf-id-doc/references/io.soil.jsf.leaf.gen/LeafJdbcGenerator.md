# LeafJdbcGenerator

> JDBC 数据库协调器，自动分配 workerId、心跳维护、降级恢复

- **包**: io.soil.jsf.leaf.gen
- **实现接口**: `ILeafGenerator`

## 说明

`LeafJdbcGenerator` 通过数据库表 `jsf_leaf_holder` 实现工作节点的自动分配和心跳维护。节点启动时根据 nodeKey（IP:Port）查询是否已有分配记录，有则复用，无则抢占空闲 worker。抢占使用乐观锁机制，防止并发场景下同一 worker 被多个节点同时选中。

内置定时心跳任务，每 5 分钟更新一次心跳时间戳，保持 worker 活跃状态。心跳超过 12 小时未更新的 worker 视为空闲可回收。

当 `jsf.leaf.holder-type` 为 `jdbc` 时，由 `LeafAutoConfig` 自动注册此实现。

## 构造

### LeafJdbcGenerator

`LeafJdbcGenerator(Integer dataCenterId, LeafHolderMapper workerMapper, String nodeKey)`

> 构造 JDBC 协调器

**参数**:
- `dataCenterId` (`Integer`) — 数据中心 ID，范围 0 ~ 31
- `workerMapper` (`LeafHolderMapper`) — 数据库 Mapper
- `nodeKey` (`String`) — 节点唯一标识（格式：IP:Port）

## 方法

### init

`void init()`

> 初始化协调器，执行节点查询/抢占/心跳启动

**异常**: `LeafIdException` — 无可用 worker 或抢占失败

### dataCenterId

`int dataCenterId()`

> 获取数据中心 ID

**返回**: `int` — 配置的数据中心 ID

### workerId

`int workerId()`

> 获取工作节点 ID

**返回**: `int` — 从数据库分配的工作节点 ID

## 示例

```yaml
# application.yml
jsf:
  leaf:
    holder-type: jdbc
    data-center-id: 0
    ip-coordinator:
      ip: 192.168.1.100
      port: 3306
```