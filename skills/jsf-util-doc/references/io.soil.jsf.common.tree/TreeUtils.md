# TreeUtils

> 树模型工具类，支持 list、tree、map 等节点在各种数据结构中的转换

- **包**: io.soil.jsf.common.tree

## 方法

### toTree

`static <ID,TYPE,R extends Node<ID,TYPE>> List<R> toTree(List<R> nodes)`

> 将 list 转换成 tree，根据 parentId 自动组装父子关系

**参数**:
- `nodes` (`List<R>`) — 扁平节点列表

**返回**: `List<R>` — 根节点列表（树结构）

### toList

`static <ID,TYPE,R extends Node<ID,TYPE>> List<R> toList(Collection<R> treeNodes)`

> 将 tree 转换成 list，展开所有子节点

**参数**:
- `treeNodes` (`Collection<R>`) — 树节点集合

**返回**: `List<R>` — 包含所有节点的扁平列表

### toMap

`static <ID,Type,R extends Node<ID,Type>> Map<ID,R> toMap(Collection<R> nodes)`

> 将 list 或 tree 转换成 map，以节点 ID 为键

**参数**:
- `nodes` (`Collection<R>`) — 节点集合（list 或 tree 均可）

**返回**: `Map<ID,R>` — 以节点 ID 为键的 Map

## 示例

```java
// list → tree
List<Node<Long,String>> tree = TreeUtils.toTree(flatList);

// tree → list
List<Node<Long,String>> flat = TreeUtils.toList(tree);

// list/tree → map
Map<Long,Node<Long,String>> map = TreeUtils.toMap(flatList);
```