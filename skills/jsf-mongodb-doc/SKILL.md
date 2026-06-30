---
name: "jsf-mongodb-doc"
description: "Use when coding with jsf-mongodb SDK, need API reference for Spring Data MongoDB base document class, Snowflake ID generation, auditing fields, or MongoDocIdCallback usage."
---

# jsf-mongodb SDK 参考

基于 Spring Data MongoDB 的通用公共模块，提供 Document 基类、Snowflake ID 自动生成、审计字段自动填充和事务管理。

## 依赖引入

Maven 工程的依赖引入参考：'[jsf-bom-doc/SKILL.md](../jsf-bom-doc/SKILL.md)'

| ArtifactId | 说明 |
|-----------|------|
| `jsf-mongodb` | MongoDB 通用公共类 |

## 核心 API

### 定义 Document

```java
// 审计人为 Long 类型（配合 AuditorAware<Long>）
@Document(collection = "users")
public class UserDoc extends BaseMongoDoc<Long> {
    @Field("name")
    private String name;
}

// 审计人为 String 类型（配合 AuditorAware<String>）
@Document(collection = "orders")
public class OrderDoc extends BaseMongoDoc<String> {
    @Field("orderNo")
    private String orderNo;
}
```

### BaseMongoDoc<U> 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `id` | `Long` | Snowflake ID，自动生成 |
| `createdAt` | `OffsetDateTime` | 创建时间（携带时区偏移） |
| `updatedAt` | `OffsetDateTime` | 更新时间（携带时区偏移） |
| `createdBy` | `U` | 创建人，类型由泛型参数决定 |
| `updatedBy` | `U` | 更新人，类型由泛型参数决定 |

### 前置条件

- 引入 `jsf-leaf-id`（Snowflake ID 来源）
- 配置 MongoDB 连接信息（`spring.data.mongodb.uri`）
- 提供 `AuditorAware<U>` Bean（由外部模块实现，泛型须与 BaseMongoDoc 匹配）

## 自动配置

`MongoAutoConfig` 在 classpath 下存在 `MongoTemplate` 时自动激活：

| Bean | 说明 |
|------|------|
| `MongoTransactionManager` | 事务管理器（`@ConditionalOnMissingBean`） |
| `MongoDocIdCallback` | Snowflake ID 自动生成回调 |

## 类索引

### io.soil.jsf.mongodb.doc

| 类 | 说明 |
|----|------|
| `BaseMongoDoc<U>` | Document 抽象基类，泛型 `<U>` 定义审计人字段类型 |
| `MongoDocIdCallback` | BeforeConvertCallback，保存前自动生成 Snowflake ID |

### io.soil.jsf.mongodb.config

| 类 | 说明 |
|----|------|
| `MongoAutoConfig` | Spring Boot 自动配置，注册事务管理器和 ID 回调 |