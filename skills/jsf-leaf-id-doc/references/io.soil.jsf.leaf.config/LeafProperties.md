# LeafProperties

> 配置属性绑定，前缀 `jsf.leaf`

- **包**: io.soil.jsf.leaf.config
- **注解**: `@Data`, `@ConfigurationProperties("jsf.leaf")`

## 属性

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `dataCenterId` | `Integer` | `null` | 数据中心 ID，范围 0 ~ 31（5 bit） |
| `ipCoordinator` | `ipCoordinator` | - | IP 协调器配置（JDBC 模式） |

## 内部类

### ipCoordinator

IP 协调器参数，通过探测本机到远程目标的出口 IP，拼接服务端口生成 nodeKey（格式：IP:Port），用于在数据库中唯一标识和区分不同工作节点。

| 属性 | 类型 | 说明 |
|------|------|------|
| `ip` | `String` | 远程目标 IP，用于探测本机到该目标的出口 IP |
| `port` | `Integer` | 远程目标端口 |

## 配置示例

```yaml
jsf:
  leaf:
    data-center-id: 0
    ip-coordinator:
      ip: 192.168.1.100
      port: 3306
```