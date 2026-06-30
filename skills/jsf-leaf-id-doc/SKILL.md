---
name: "jsf-leaf-id-doc"
description: "Use when coding with jsf-leaf-id SDK, need API reference for distributed unique ID generation, Snowflake ID, workerId coordination, dataCenterId, or LeafId usage."
---

# jsf-leaf-id SDK 参考

基于 Snowflake 算法的分布式唯一 ID 生成组件，支持静态配置和 JDBC 数据库两种工作节点协调方式。

## ID 结构

```
| 1 bit  |       42 bit        |   5 bit    |   8 bit    |   8 bit   |
| 符号位  |  时间戳（相对 EPOCH） |  数据中心ID  |  工作节点ID  |  毫秒内序号  |
|   0    |  约 139 年可用        |  0 ~ 31    |  0 ~ 255   |  0 ~ 255  |
```

- EPOCH：2026-01-01 00:00:00 UTC
- 单节点 QPS：约 25.6 万/秒

## 依赖引入

Maven 工程的依赖引入参考：'[jsf-bom-doc/SKILL.md](../jsf-bom-doc/SKILL.md)'

| ArtifactId | 说明 |
|-----------|------|
| `jsf-leaf-id` | 分布式唯一 ID 生成 |

JDBC 模式需额外引入 `mybatis-spring-boot-starter` 和 `mysql-connector-j`。

## 核心 API

### 生成 ID

```java
long id = LeafId.nextId();
```

唯一需要调用的方法，线程安全，全局静态。

## 配置项

| 配置项 | 默认值 | 说明 |
|--------|--------|------|
| `jsf.leaf.holder-type` | `default` | `default`（静态 workerId）/ `jdbc`（数据库协调） |
| `jsf.leaf.data-center-id` | `0` | 数据中心 ID，范围 0 ~ 31（5 bit） |
| `jsf.leaf.worker-id` | `0` | 静态模式的 workerId，范围 0 ~ 255（8 bit） |
| `jsf.leaf.ip-coordinator.ip` | - | JDBC 模式：远程目标 IP，用于探测本机出口 IP |
| `jsf.leaf.ip-coordinator.port` | - | JDBC 模式：远程目标端口 |

JDBC 模式需先执行建表脚本 `script/mysql/init.sql`。

## 类索引

### io.soil.jsf.leaf

| 类 | 说明 |
|----|------|
| `IDGen` | ID 生成器顶层接口 |
| `LeafAutoConfig` | Spring Boot 自动配置，按 holder-type 注册协调器 Bean |
| `LeafId` | 静态工具门面，提供 `nextId()` 全局入口 |

### io.soil.jsf.leaf.gen

| 类 | 说明 |
|----|------|
| `ILeafGenerator` | 工作节点协调器接口，提供 `dataCenterId()` 和 `workerId()` |
| `LeafDefaultGenerator` | 静态 dataCenterId + workerId 协调器（默认） |
| `LeafJdbcGenerator` | JDBC 数据库协调器，自动分配/心跳/降级恢复 |
| `LeafIdGenImpl` | Snowflake ID 生成器核心实现（1+42+5+8+8 bit） |

### io.soil.jsf.leaf.config

| 类 | 说明 |
|----|------|
| `LeafProperties` | 配置属性绑定（`jsf.leaf` 前缀），含 `dataCenterId` |

### io.soil.jsf.leaf.exception

| 类 | 说明 |
|----|------|
| `LeafIdException` | Leaf 异常，封装时钟回拨/workerId 越界/dataCenterId 越界/抢占失败等 |

### io.soil.jsf.leaf.mapper

| 类 | 说明 |
|----|------|
| `LeafHolderMapper` | 工作节点 Mapper，操作 `jsf_leaf_holder` 表 |
| `LeafHolderPO` | 工作节点 PO |