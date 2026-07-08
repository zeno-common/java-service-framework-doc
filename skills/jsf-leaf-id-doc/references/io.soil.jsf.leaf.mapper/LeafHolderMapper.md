# LeafHolderMapper

> 工作节点 Mapper，操作 `jsf_leaf_holder` 表

- **包**: io.soil.jsf.leaf.mapper
- **注解**: `@Mapper`

## 说明

`LeafHolderMapper` 操作 `jsf_leaf_holder` 表，提供工作节点的查询、抢占和心跳更新功能。配合 `LeafJdbcGenerator` 实现基于数据库的 workerId 协调。

## 方法

### getWorkerIdByNodeKey

`LeafHolderPO getWorkerIdByNodeKey(String nodeKey)`

> 根据节点标识查询工作节点记录，用于节点重启时复用之前分配的 workerId

**参数**:
- `nodeKey` (`String`) — 节点唯一标识（IP:Port）

**返回**: `LeafHolderPO` — 工作节点记录，不存在则返回 null

### getOneWorkerBefore

`LeafHolderPO getOneWorkerBefore(Long timestamp)`

> 查询一个心跳时间早于指定时间戳的空闲工作节点（带行锁 FOR UPDATE）

**参数**:
- `timestamp` (`Long`) — 心跳阈值时间戳，早于此时间的 worker 视为空闲

**返回**: `LeafHolderPO` — 空闲的工作节点记录，无可用节点时返回 null

### occupyWorker

`Boolean occupyWorker(Integer id, String nodeKey, Long lastHeartBeat, Long timestamp)`

> 使用乐观锁抢占工作节点，以 lastHeartbeat 作为版本号

**参数**:
- `id` (`Integer`) — 工作节点 ID
- `nodeKey` (`String`) — 当前节点的唯一标识
- `lastHeartBeat` (`Long`) — 乐观锁版本号（上次心跳时间戳）
- `timestamp` (`Long`) — 新的心跳时间戳

**返回**: `Boolean` — 抢占成功返回 true，版本号不匹配返回 false

### updateLastHeartbeat

`Boolean updateLastHeartbeat(Integer id, Long timestamp)`

> 更新工作节点的心跳时间戳，由定时心跳任务调用

**参数**:
- `id` (`Integer`) — 工作节点 ID
- `timestamp` (`Long`) — 当前时间戳

**返回**: `Boolean` — 更新成功返回 true