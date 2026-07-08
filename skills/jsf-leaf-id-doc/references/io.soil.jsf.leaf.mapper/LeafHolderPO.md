# LeafHolderPO

> 工作节点持有者持久化对象，对应 `jsf_leaf_holder` 表

- **包**: io.soil.jsf.leaf.mapper.po
- **注解**: `@Data`

## 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | `Integer` | 工作节点 ID，即 Snowflake 算法中的 workerId，范围 0 ~ 255 |
| `nodeKey` | `String` | 占用此 worker 的节点唯一标识，格式为 IP:Port |
| `lastHeartbeat` | `Long` | 上一次心跳时间戳（毫秒），用于判断 worker 是否仍在使用中 |
| `createTime` | `Date` | 记录创建时间 |