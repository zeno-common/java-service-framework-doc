# Node

> 通用树节点定义，支持泛型的节点 ID 和类型

- **包**: io.soil.common.tree
- **泛型**: `<ID>` 节点标识类型, `<TYPE>` 节点类型
- **Lombok**: `@Data` — 所有字段均有 getter/setter [Lombok 生成]

## 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `id` | `ID` | 节点标识 |
| `name` | `String` | 节点名称 |
| `type` | `TYPE` | 节点类型 |
| `parentId` | `ID` | 父节点标识，null 表示顶级节点 |
| `ordinal` | `Number` | 节点序数 |
| `addition` | `Object` | 扩展部分 |
| `children` | `Collection<Node<ID,TYPE>>` | 子节点列表 |

## 方法

### addChild

`void addChild(Node<ID,TYPE> node)`

> 添加子节点，首次添加时自动初始化子节点列表

**参数**:
- `node` (`Node<ID,TYPE>`) — 要添加的子节点

## 示例

```java
Node<Long, String> root = new Node<>();
root.setId(1L);
root.setName("根节点");
root.setType("FOLDER");

Node<Long, String> child = new Node<>();
child.setId(2L);
child.setName("子节点");
child.setParentId(1L);

root.addChild(child);
```