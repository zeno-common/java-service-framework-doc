# LeafDefaultGenerator

> 静态 dataCenterId + workerId 协调器（默认模式）

- **包**: io.soil.jsf.leaf.gen
- **实现接口**: `ILeafGenerator`

## 说明

`LeafDefaultGenerator` 是最简单的协调器实现，直接使用配置文件中指定的 dataCenterId 和 workerId。适用于单节点部署或手动分配工作节点的场景。

当 `jsf.leaf.holder-type` 为 `default` 或未配置时，由 `LeafAutoConfig` 自动注册此实现。

## 构造

### LeafDefaultGenerator

`LeafDefaultGenerator(Integer dataCenterId, Integer workerId)`

> 构造静态协调器

**参数**:
- `dataCenterId` (`Integer`) — 数据中心 ID，范围 0 ~ 31
- `workerId` (`Integer`) — 工作节点 ID，范围 0 ~ 255

## 方法

### dataCenterId

`int dataCenterId()`

> 获取数据中心 ID

**返回**: `int` — 配置的数据中心 ID

### workerId

`int workerId()`

> 获取工作节点 ID

**返回**: `int` — 配置的工作节点 ID

## 示例

```yaml
# application.yml
jsf:
  leaf:
    holder-type: default
    data-center-id: 0
    worker-id: 1
```